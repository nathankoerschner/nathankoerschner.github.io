## nicequestions.com

<img src="/assets/images/nicequestions-screenshot.png" alt="The nicequestions.com homepage showing a masonry grid of beautiful photographs, each paired with a thoughtful question" style="width: 100%; border-radius: 8px; margin-bottom: 20px;">
<p style="font-size: 0.85em; color: #666; margin-top: -15px; margin-bottom: 30px;">The homepage: a masonry grid of community-submitted questions paired with curated photography</p>

[nicequestions.com](https://nicequestions.com) is a community-driven site where anyone can submit a thoughtful question. Each question gets paired with a photograph and displayed in a browsable masonry grid. Questions are organized into categories like "For Crossroads," "For Loved Ones," "Making Friends," "Big Questions," "For A Gathering," and "Meet Yourself."

I built it over a weekend in January 2026 using Next.js, Firebase, and a couple of external APIs.

## The LLM Gate

The core moderation challenge: how do you let anyone submit a question while keeping the quality bar high, without manual review?

The answer is an LLM gate. Every submission gets sent to OpenAI's GPT-4o-mini before it touches the database. The model checks whether the submission is actually a question (rejecting statements, commands, and gibberish), screens for harmful content, and filters spam. It's deliberately permissive—the goal is to keep the door open for creative and unexpected questions while catching the obvious junk.

When a question passes, the model also cleans up grammar and punctuation and assigns it to one of the six categories. The whole validation, cleanup, and categorization happens in a single API call with structured JSON output at a low temperature for consistency.

## Where the Images Come From

Each accepted question gets paired with a random photograph pulled from a curated Unsplash collection of film-style photography (2300+ photos). The images aren't hotlinked—they're downloaded as buffers and uploaded to Firebase Storage. This means the site doesn't depend on Unsplash's CDN at runtime, and the images persist even if the original Unsplash photos are removed.

The app also tracks each photo's Unsplash ID in the database to prevent the same image from appearing twice.

## The Database

There's no traditional database here—everything lives in Firestore. Each question is a document with the question text, its assigned category, the Firebase Storage image URL, the Unsplash photo ID, and a timestamp. A separate config document tracks daily submission limits (200 attempts and 200 accepted questions per day) as a simple abuse prevention measure.

## Stack

- **Next.js** (App Router) on **Vercel**
- **Firebase** (Firestore + Storage)
- **OpenAI** GPT-4o-mini for question validation
- **Unsplash API** for sourcing images
- **Tailwind CSS** for styling

The whole thing is anonymous—no user accounts, no authentication. Just a text box, an AI gatekeeper, and a growing collection of questions worth asking.

## Building with OpenClaw

During this project I was trying out OpenClaw, and it was quite amazing to use the app on my phone and send text messages to have the app debugged.
