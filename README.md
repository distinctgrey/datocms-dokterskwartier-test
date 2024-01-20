# Dokterskwartier TEST

This project is a proof-of-concept for the combination of SvelteKit, DatoCMS and Netlify.  
It started from the DatoCMS SvelteKit starter kit.

## Preview mode and deploy environment

To take advantage of preview mode, deploy environment must support edge functions. That shouldn't be an issue: most of the providers have some form of edge function, these days.

## Safety check before production

If you use this demo as a starting point for a project and you plan to deploy to production, **take some time to understand how to properly configure secrets, so that no reserved information (like, for example, DatoCMS contents in draft status) gets leaked**.

Before deploying to production, you should set the following 4 environment variables:

- `PREVIEW_MODE_PASSWORD`: the password that users must have to enable preview mode;
- `PUBLIC_DATOCMS_API_TOKEN`: a DatoCMS token with read-only permissions and no access to draft contents: this token can be included in the bundles produced by Nuxt at deploy;
- `DRAFT_ENABLED_DATOCMS_API_TOKEN`: a DatoCMS token with read-only permissions and **access to draft contents**: this token will be potentially accessible only to users who have access to the preview mode (thus, only to people that know the preview mode password and are therefore expected to see draft contents);
- `PREVIEW_MODE_ENCRYPTION_SECRET`: this secret is meant to sign the cookie that enables preview mode: it can be any random string.

With these secrets in place, you can safely go to production.

## Local setup

Once the setup of the project and repo is done, clone the repo locally.

### Set up environment variables

In your DatoCMS' project, go to the **Settings** menu at the top and click **API tokens**.

Then click **Bundle-safe, read-only token** and copy the token.  
Do the same for the **Draft-enabled, read-only token**.

Next, copy the `.env.example` file in this directory to `.env` (which will be ignored by Git):

```bash
cp .env.example .env
```

Then set each variable in `.env`.

### Developing your project locally

Install dependencies:

```bash
nvm use
npm install
```

Start a development server:

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

## Building

To create a production version of your app:

```bash
npm run build
```

You can preview the production build with `npm run preview`.
