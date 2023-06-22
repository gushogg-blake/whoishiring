## HN 'Who is hiring?' better job board

I'm using SvelteKit to make this app!

It takes all the job posts from the latest monthly HN 'Who is hiring' post, and delivers, I hope, a way better user interface.

## June 21, 2023

Started designing my site in Figma! Still a work in progress. You can find my scrapbook-like design board live in Figma [here](https://www.figma.com/file/6oFzUK7XW7ZraniN5Yu0so/whoishiring?type=design&node-id=0%3A1&t=o6l0XFyVDSyPRLKu-1).

<img width="787" alt="design" src="https://github.com/hazzelnut/whoishiring/assets/6500879/4c387844-cb8a-47f6-af55-ff28ee534e80">


## June 16, 2023

I've been working on migrating the original stack over to Fly.io. Originally, my setup was: SvelteKit + Supabase DB (and its DB API) + Supabase Edge functions. Everything worked great and the MVP was finished. But, there was one problem.

The Supabase edge function was triggered by a cron job every 5 minutes, and the edge function would fetch data from the HN API and insert it into the DB. After a few days, I checked on my usages and found that I had exceeded my free database egress limit! That prompted me to look for alternative solutions. And oddly, the database usage bar was also slowly increasing even though I was only updating rows at the time and not adding more to the table. I wish I had a screenshot to show the bright red warnings, but it was clear that using Supabase wasn't viable going forward (for freeness sake).

After researching and testing out other possible solutions, my new stack became: SvelteKit + Drizzle ORM + Fly.io Postgres + Fly.io Machine. Fly.io's free tier was much more generous and I was also able to deploy and host the site on their platform too which was a big plus.

The biggest win is for me in this new setup is that I can support all the functionality for free without running into limits (yet!) and I'll probably continue with it until I need to upgrade or scale it.

You can find the rough version currently at [whoishiring-app.fly.dev](https://whoishiring-app.fly.dev)

My simple fly.io setup:
<img width="1009" alt="fly io setup" src="https://github.com/hazzelnut/whoishiring/assets/6500879/bdf19580-226e-4adb-abd8-2f57787bdc98">


## May 18, 2023
We have tags! Now you can filter job posts by popular tags or keywords found across all the posts.

https://github.com/hazzelnut/whoishiring/assets/6500879/3d4123df-e8d2-4826-bec9-184e7ff6a6bf


## April 29, 2023
Here's a sneak peek! It has the basic sort and search functionality and infinite scroll!
The final version will be much more beautiful, I promise.

https://user-images.githubusercontent.com/6500879/235334665-304fd248-45f1-40dd-9753-c747ecfe1c1c.mp4

# Deploying to Fly.io

1. Install flyctl and login, see [here](https://fly.io/docs/hands-on/install-flyctl/)
2. Update your adapter in svelte.config.js to use `adapter-node`, see [here](https://kit.svelte.dev/docs/adapter-node)
3. Add a start script in your package.json. 
  ```js
    // Have environment variables you need need in production? Run 'npm install dotenv'
		"start": "node -r dotenv/config build"
    // Or, if you don't need environment variables
		"start": "node build"
  ```
4. Run `fly launch`. It will guide you through the process of deploying your app.
5. Done! Navigate to your new site at `<name_of_app>.fly.dev`
