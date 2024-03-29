# Next.js Subscription Payments Starter

The all-in-one starter kit for high-performance SaaS applications. With a few clicks, Next.js developers can clone, deploy and fully customize their own SaaS subscription application.

## Features

- Secure user management and authentication with [Supabase](https://supabase.io/docs/guides/auth).
- Powerful data access & management tooling on top of PostgreSQL with [Supabase](https://supabase.io/docs/guides/database).
- Integration with [Stripe Checkout](https://stripe.com/docs/payments/checkout) and the [Stripe customer portal](https://stripe.com/docs/billing/subscriptions/customer-portal), all plumbing already set up.
- Automatic syncing of pricing plans, and subscription statuses via [Stripe webhooks](https://stripe.com/docs/webhooks).

## Demo

- https://nextjs-subscription-payments-cjavilla-stripe.vercel.app/

[![Screenshot of demo](./public/demo.png)](https://nextjs-subscription-payments-starter.vercel.app/)

## Architecture

![Architecture diagram](./public/architecture_diagram.svg)

## Setup

### 1. Create new Supabase project

Sign up to Supabase - [https://app.supabase.io](https://app.supabase.io) and create a new project. Wait for your database to start.

### 2. Set up your database tables and auth policies

In your Supabase dashboard, go to the SQL editor. There, the welcome tab has a "Quick Start" section. Select the "Stripe Subscriptions" quick start (it has the same content as the [`schema.sql` file](./schema.sql)) and hit the "RUN" button.

#### [Optional] - Set up OAuth providers

You can use third-party login providers like GitHub or Google. Refer to the [docs](https://supabase.io/docs/guides/auth#third-party-logins) to learn how to configure these.

### 3. Get your Supabase credentials

In your [Supabase Dashboard](https://app.supabase.io/), go to the Project Settings (the cog icon), open the API tab, and find your API URL, the public `anon` key, and the secret `service_role` key. You will be prompted for these when deploying with Vercel.

## Deploy with Vercel

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/git/external?repository-url=https%3A%2F%2Fgithub.com%2Fthorwebdev%2Fnextjs-subscription-payments&env=NEXT_PUBLIC_SUPABASE_URL,NEXT_PUBLIC_SUPABASE_ANON_KEY,SUPABASE_SERVICE_ROLE_KEY&envDescription=Add%20your%20API%20keys%20from%20the%20Supabase%20Dashboard&project-name=nextjs-subscription-payments&repo-name=nextjs-subscription-payments&demo-title=Next.js%20Subscription%20Payments%20Starter%20Demo&demo-url=https%3A%2F%2Fnextjs-subscription-payments-starter.vercel.app%2F&demo-image=https%3A%2F%2Fnextjs-subscription-payments-starter.vercel.app%2Fdemo.png&integration-ids=oac_pb1dqJT8Ry2D99Q0o9qXWIhJ)

Once your project has been deployed, continue with the configuration steps below.

### Configure Supabase Auth

After deploying, copy the deployment URL and navigate to your Supabase project settings (Authentication > Settings) and set your site url.

## Configure Stripe

### Create product and pricing information

For Stripe to automatically bill your users for recurring payments, you need to create your product and pricing information in the [Stripe Dashboard](https://dashboard.stripe.com/test/products). When you create or update your product and price information, the changes are automatically synced with your Supabase database, as long as the webhook is configured correctly as described above.

Stripe Checkout currently supports pricing plans that bill a predefined amount at a specific interval. More complex plans (e.g. different pricing tiers or seats) are not yet supported.

For example, you can create business models with different pricing tiers, e.g.:

- Product 1: Hobby
  - Price 1: 10 USD per month
  - Price 2: 100 USD per year
  - Price 3: 8 GBP per month
  - Price 4: 80 GBP per year
  - [...]: additional currency and interval combinations
- Product 2: Freelancer
  - Price 1: 20 USD per month
  - Price 2: 20 USD per year
  - Price 3: 16 GBP per month
  - Price 4: 160 GBP per year
  - [...]: additional currency and interval combinations

### Configure the Stripe customer portal

1. Set your custom branding in the [settings](https://dashboard.stripe.com/settings/branding).
1. Configure the Customer Portal [settings](https://dashboard.stripe.com/test/settings/billing/portal).
1. Toggle on "Allow customers to update their payment methods".
1. Toggle on "Allow customers to update subscriptions".
1. Toggle on "Allow customers to cancel subscriptions".
1. Add the products and prices that you want to allow customer to switch between.
1. Set up the required business information and links.

## That's it

That's it, you're now ready to earn recurring revenue from your customers \o/
