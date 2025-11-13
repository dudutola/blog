---
title:  "Async vs Sync Requests | From Static Data to OpenAi Images"
date:   2025-11-13
tags: [javascript, requests, synchronous, asynchronous, promises, openai, frontend]
---
<!-- link para site -->
App link → [Sync vs Async Requests](https://dulcelene.com/sync-and-async-requests/)
<!-- [https://dulcelene.com/sync-and-async-requests/](https://dulcelene.com/sync-and-async-requests/) -->

These days, I’ve been trying to better understand how **promises** work, especially when I need to make **multiple image requests** asynchronously without waiting for each one to finish before starting the next.

To learn it properly, I decided to build a small app to test the difference between synchronous and asynchronous requests using both static data and OpenAI API calls.

<!-- --- -->

### Step 1: Static Data Mode
I started simple: a test mode using static data to simulate requests.
Everything worked smoothly, the sync version was clear and easy to follow.

<!-- --- -->

### Step 2: OpenAI Mode — Sync Version

Next, I tried to apply the same logic with OpenAI image requests.
The first problem I faced was retrieving image data, I was using `FileReader`, to get the image source (URL) for my `fetch` requests.

After thinking (a lot 😅), I realized something simple but crucial:
- when uploading files, we already have access to the `<img>` tags, so I could just select all images and get their `src` attributes.
It worked perfectly!

<!-- --- -->

### Step 3: OpenAI Mode — Async Version

Then I moved to the asynchronous version.
Using `Promise.allSettled()`, I was able to handle all image requests at the same time, check results, and manage errors more cleanly.
It worked great, much faster and more efficient.

Quick note on promises:
- **Promise.all()** waits for all promises to succeed, if any fail, it stops and rejects immediately
- **Promise.allSettled()** waits for all promises to finish, whether they succeed or fail, giving you a result for each.

---
&nbsp;

#### Improvements:

Once the logic worked, I started refining the app:
- the image captions (`<p>`) were initially empty, so I added a temporary message “Describing image…” to show that analysis is in progress.
- displayed the total time for image processing in OpenAI mode
- created reusable function `showTotalTime(startTime)` to calculate and display how long each request takes and to avoid repeating code
- added small styling updates to clearly separate each section (static vs API)

<!-- --- -->

#### Next Steps:

- [ ] Add spinners on the images while processing
- [ ] Move repeated fetch logic into shared functions
- [ ] Decide between using `for` or `map` loops consistently across openai mode
- [ ] Continue improving layout and structure

<!-- --- -->

Building this helped me understand promises much better, especially how async operations really flow compared to sync ones. It’s always nice when theory turns into something visual and practical.
