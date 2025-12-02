---
title:  "Async Jobs, Multi-Image Processing & Rails Adventures"
date:   2025-12-02
tags: [rails, background-jobs, api, faraday, heroku]
---

These past weeks I’ve been deep into **background jobs in Rails**, trying to make everything work with **multi-image uploads and AI processing**. I learned so much, but it was a wild ride.

<!-- --- -->

### The Network Errors Saga

At first, everything seemed fine… until I started sending 3 images at once. Two would work, and one would fail with this classic Faraday/TCP error:

```
Network error: Failed to open TCP connection
execution expired
```

I thought the API was acting up, but it turned out the problem was mostly **our free-tier Heroku plan hitting limits**. My colleague suggested upgrading the plan to avoid “cold call” errors.

After the upgrade, those network errors mostly disappeared. I also updated the **code, procfile, dynos, workers, and Sidekiq setup**, all the new stuff to make it work reliably.

<!-- --- -->

### The Double Results Mystery

Even after fixing network issues, I started seeing **duplicate results**.

I investigated and realized the problem was in the `create` action:

* I was attaching images twice. First, from the params:

```rb
@diagnosis = Diagnosis.new(diagnosis_params)
```

* Then I tried to attach again from the existing Active Storage blobs:

```rb
images = Array(params.dig(:diagnosis, :images)).reject(&:blank?)
@diagnosis.images.attach(images) # ❌ duplicates
```

So yes… **the duplicates were all my fault** 😅

✅ Fix: only attach new images, don’t reattach what’s already there. Problem solved.

<!-- --- -->

### Heroku, Redis & Sidekiq Tweaks

After that, there were still a few Heroku-specific issues:

* Redis & Sidekiq configuration needed updates to support **Turbo Streams** and background jobs properly.
* After adding the necessary gems and restarting dynos, the app finally worked reliably.

---
&nbsp;

### Report Generation With Multiple Images

Here came a tricky part:

Previously, with only **one image**, the report generated automatically after processing. But now with **multiple images**, I didn’t know when all the jobs were finished.

Ideas I considered:

* Counting images and checking when all are processed
* Using another background job to generate the report
* Waiting for a Rails callback when the last job finishes

For now, I went with the **simplest solution**: a **button** that the user clicks to generate the report after everything is done. Not automatic yet, but it works reliably.

---
&nbsp;

#### Lessons Learned

* **Multi-image uploads + background jobs** can be tricky with Rails
* **Active Storage** duplicates easily if you’re not careful
* **Network errors** can come from Heroku plan limits, not just your code

<!-- --- -->

#### Next Steps

- [ ] Find a **better solution to automatically generate the report** without extra clicks
- [ ] Improve **error handling** when some images fail
- [ ] Retry failed jobs automatically
- [ ] Add **request logs and durations** for better debugging

It’s fun and challenging to think about how Rails handles async stuff compared to JavaScript promises. Every solution has trade-offs, and figuring out which one works best for multi-image AI processing is a real learning experience 😅
