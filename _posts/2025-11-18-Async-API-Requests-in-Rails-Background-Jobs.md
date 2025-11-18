---
title:  "Async API Requests in Rails | Multi-Image Processing with Background Jobs"
date:   2025-11-18
tags: [ruby, rails, background-jobs, api, faraday]
---

These past few days I’ve been experimenting with **synchronous vs asynchronous requests**, but this time inside a **Ruby on Rails app** instead of JavaScript.
My goal was simple:
**send multiple images → get AI-generated captions → test sync and async behavior → handle failures properly.**

I already had a tiny Rails app that worked with simple data, so I decided to expand it and make it process real images using the OpenAI API.

<!-- --- -->

### Step 1: First Tests in Rails (Sync & Async)

I first built a small proof-of-concept that sends images to OpenAI using **Faraday**, one at a time.
This helped me understand how Rails handles multiple uploads and how to structure my API calls.

Everything was okay until I introduced **multiple images + background jobs**…

…and that’s where all the issues started 😅

<!-- --- -->

### Step 2: Fixing My API Request (the /v1 mistake)

At first, my request didn’t work at all:
```rb
conn = Faraday.new(
  url: "https://api.openai.com/v1",  # ❌ wrong
)
```

Because later I was doing:
```rb
conn.post("/chat/completions")
```

So the final URL became:
```
https://api.openai.com/v1/chat/completions
```

But OpenAI expects:
```
https://api.openai.com/v1/chat/completions
```
So far, that looks correct… BUT:
Faraday handles slashes in a strict way. If the base URL ends with /v1 and the request begins with /chat/..., Faraday assumes the request path is absolute, and DOES NOT prepend /v1.

Meaning:
```
https://api.openai.com/chat/completions
```

No wonder it was failing 😭
I fixed it by removing `/v1` from the base URL:

```rb
conn = Faraday.new(
  url: "https://api.openai.com",     # ✅ correct
)
```

Then all good again.

---
&nbsp;

## Principal App testing

### Step 3: Background Jobs Chaos: Only Saving the Last Result

I was sending 2–3 images, but only the *last* one was being saved in the JSON column.
Classic **race condition**.

Solution:

#### ➜ I added a **row-level lock** so updates don’t overwrite each other:

```rb
diagnosis.with_lock do
  # safely update attributes here
end
```

After adding this, Rails stopped losing updates and every image result was saved properly.

### Step 4: Timeout Issues & Network Errors

When testing with 3 images, I started getting this:

```
Network error: Failed to open TCP connection
execution expired
```

Classic Faraday timeout.
So I increased the limits:

```rb
conn = Faraday.new(
  url: url,
  request: {
    open_timeout: 15,
    timeout: 60
  }
)
```

This helped, but I still saw occasional failure for 1 out of 3 images.

At first I thought the API was down, but then I realized:
**processing 3 heavy images in parallel is expensive**, and some requests simply take longer.


### Step 5: Handling Partial Failures (1 fails, 4 succeed)

At first I tried showing an `alert` **inside the job**, but of course you can’t show UI from a background worker.

Then I tried checking the job result on `create`, but:

* `perform_later` does **not** return a result
* it’s normal that some images succeed and others fail
* blocking the user from moving forward is a bad UX

So I decided on a different approach:

* ✔️ Always redirect to the diagnosis page

* ✔️ Show all images that succeeded

* ✔️ Show an inline error only in the results section, or as an alert

Something like:

> *“1 image failed to process. You can retry individually after.”*

This feels more natural, and the flow continues without blocking the user.

---
&nbsp;

#### Next Steps:

* [ ] Improve error handling when some images fail
* [ ] Maybe retry failed jobs automatically
* [ ] Add request logs + request duration tracking
* [ ] Reintroduce “report” and “comparison” features
* [ ] Test increasing Faraday timeout for 3+ images


Building this system helped me understand in practice how Rails handles:

* concurrency
* Active Job behavior
* row-level locking to avoid lost updates
* network timeouts
* multi-image uploads
* partial failures

It’s really different from JavaScript promises, but the concepts of sync vs async are still there, just expressed in a Rails way.
