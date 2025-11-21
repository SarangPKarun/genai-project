# AI News Aggregator - Live Build Repository

This repository accompanies my 3-hour live coding session where I build a complete AI-powered news aggregator from scratch. This is a **private repository** containing valuable implementation details and deployment strategies used in production environments.

## Project Structure

This project is organized across three branches, each corresponding to a different phase of the build:

- **`master`** - Part 1: Local setup and core functionality
- **`deployment`** - Part 2: Deployment configuration and infrastructure
- **`deployment-final`** - Part 3: Final optimizations and production-ready changes

Each branch serves as an intermediate checkpoint, allowing you to reference the exact state of the codebase at any point during the video.

## How This Video Works

This is a **live coding build**, not a traditional step-by-step tutorial. Here's what to expect:

- **Fast-paced development** - I code at my natural pace, leveraging AI tools extensively
- **AI-assisted workflow** - You won't see every code snippet or file generation in real-time
- **Real-world approach** - This condenses 20-40 hours of learning into a single session
- **Not cookie-cutter** - Unlike structured tutorials, this reflects how coding actually happens in practice

## How to Follow Along

### Recommended Approach (Maximum Learning)

1. **Clone this repository** before starting the video
2. **Keep a local copy ready** on your system as you code along
3. **Use intermediate checkpoints** - When I make major updates or run tests, pause and:
   - Reference the corresponding branch in this repository
   - Copy relevant code snippets into your project
   - Use AI coding assistants to help you reach the same checkpoint
4. **Iterate step-by-step** - Don't rush ahead. Ensure each phase works before moving forward
5. **Expect confusion** - Some parts will move fast and may not be immediately clear. This is where real learning happens

### Alternative Approach (Not Recommended)

You can skip ahead to the `deployment-final` branch and try to get everything working, but you'll miss the iterative problem-solving process that makes this valuable.

## Why This Approach?

Traditional tutorials show you the "right way" to do things. This video shows you the **real way** - with AI assistance, rapid iteration, debugging, and adapting on the fly. By following along and hitting the same checkpoints, you'll:

- Learn how to effectively leverage AI coding tools
- Understand the thought process behind architectural decisions
- Experience real-world development workflows
- Build muscle memory through hands-on practice

**The most valuable learning happens when you struggle, reference the code, and push through to the next checkpoint.**


## PROMPT

So what I want to build is an Al news aggregator where I can take multiple sources. So for example, YouTube channels. And I want, for example, blog posts from OpenAl and Emtropic. And I want to scrape those, put them into a database where we have some kind of structure where we have sources, we have, let's call them articles. And then what I want to do is I want to run a daily digest where we're going to take all of the articles from within the timeframe, and we're going to do an LLM summary around that. And then based on the user insights that we specify in some kind of like agent system prompt, we can generate a daily digest, which is going to be short snippets with a link to the original source. Now from the YouTube channels, I want to be able to create a list of channels and then we want to get the latest videos from those channels. I think we can use the youtube RSS feed for that and for the blog posts we can just have URLs that we can scrape for that. Okay, so I want everything built in a Python backend. I want to use a PostgreSQL database. I want to use SQLAlchemy in order to define the database models and then to also create the tables. I want the project structure to be an app folder where all of the app logic is in. And then I also want a Docker folder where we first create a very minimal setup And then that will probably be starting point. We want to make sure that later down the line, we can easily deploy the whole app to render and then also schedule it every 24 hours to run the reports, get everything. And then when we've created the daily digest, I want to send an email to my personal inbox with this. So that's what I have in mind. I think that would be pretty cool to build


# AI News Aggregator

## Goal Description
Build a Python-based AI news aggregator that collects content from YouTube channels (via RSS) and blog posts (via scraping), stores them in a PostgreSQL database, generates a daily digest using an LLM, and emails the summary to the user.

## Prerequisites
> [!IMPORTANT]
> **LLM Provider**: You must provide an API key for the LLM provider (e.g., OpenAI, Anthropic).

> [!IMPORTANT]
> **Email Settings**: You must provide SMTP credentials (server, port, user, password) via environment variables for the notification system.

## Implementation Steps

### 1. Project Structure
- Create a `docker-compose.yml` file to define the `db` (Postgres) and `app` services.
- Create a `docker/Dockerfile` for the Python environment setup.

### 2. Database Layer
- Create `app/models.py` to define SQLAlchemy models:
    - `Source`: ID, name, url, type (youtube/blog), active status.
    - `Article`: ID, source_id, title, url, content/summary, published_date, created_at.
- Create `app/database.py` to handle the SQLAlchemy engine and session setup.

### 3. Application Logic
- Create `app/ingestor.py`:
    - Implement `fetch_youtube_videos(source_url)` to parse RSS feeds.
    - Implement `scrape_blog_posts(source_url)` to scrape content.
- Create `app/summarizer.py`:
    - Implement `summarize_articles(articles)` to send content to the LLM.
    - Implement `generate_digest(summaries)` to format the email body.
- Create `app/notifier.py`:
    - Implement `send_email(subject, body)` to send the digest.
- Create `app/main.py`:
    - Implement the main entry point to trigger: Ingest -> Summarize -> Notify.

### 4. Verification
- Verify tables are created in Postgres.
- Run the ingestor and check for new articles.
- Check logs for generated summaries.
- Verify email delivery.

