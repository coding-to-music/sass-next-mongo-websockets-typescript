# sass-next-mongo-websockets-typescript

# 🚀 Build your own SaaS business with SaaS boilerplate. Productive stack: React, Material-UI, Next, MobX, WebSockets, Express, Node, Mongoose, MongoDB. Written with TypeScript. 🚀

https://github.com/coding-to-music/sass-next-mongo-websockets-typescript

https://sass-next-mongo-websockets-typescript.vercel.app

From / By https://github.com/async-labs/saas

https://saas-app.async-await.com/

## Environment variables:

```java
```

## GitHub

```java
git init
git add .
git remote remove origin
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:coding-to-music/sass-next-mongo-websockets-typescript.git
git push -u origin main
```

## SaaS Boilerplate

Open source web app that saves you many days of work when building your own SaaS product. The boilerplate comes with many basic SaaS features (see [Features](https://github.com/async-labs/saas#features) below) so that you can focus on features that differentiate your product.

If you want to learn how to build this project from scratch, check out our book: https://builderbook.org/book

The open source project is located in the `saas` folder. If you purchased our book, codebases for each of the book's chapters are located in the `book` folder.


## Live demo:

- APP: https://saas-app.async-await.com
- API: https://saas-api.async-await.com

## Sponsors

[![aws-activate-logo](https://user-images.githubusercontent.com/26158226/138565715-4311ddda-fb77-452a-8755-d53eb18f8645.png)](https://aws.amazon.com/activate/)

[![1password-logo](https://user-images.githubusercontent.com/26158226/138565841-ad435374-7330-477a-b6f3-2542109c3217.png)](https://1password.com/)

## Showcase

Check out projects built with the help of this open source app. Feel free to add your own project by creating a pull request.

- [Async](https://async-await.com/): Open source web app for team communication, separate urgent vs. non-urgent conversations.
- [workinbiotech.com](https://workinbiotech.com): Work in biotech, job board for small and young biotech companies
- [Retaino](https://retaino.com) by [Earl Lee](https://github.com/earllee): Save, annotate, review, and share great web content. Receive smart email digests to retain key information.
- [Builder Book](https://github.com/async-labs/builderbook): Open source web app to publish documentation or books.


## Contents

- [Features](#features)
- [Run locally](#running-api-locally)
- [Deploy](#deploy-to-heroku-aws-elastic-beanstalk-api-gateway-and-aws-lambda)
- [Built with](#built-with)
- [Screenshots](#screenshots)
- [Contributing](#contributing)
- [Team](#team)
- [License](#license)
- [Project structure](#project-structure)

## Features

- Server-side rendering for fast initial load and SEO.
- User authentication with Google OAuth API and Passwordless, cookie, and session.
- Production-ready Express server with compression, parser, and helmet.
- Transactional emails (`AWS SES`): welcome, team invitation, and payment.
- Adding email addresses to newsletter lists (`Mailchimp`): new users, paying users.
- File upload, load, and deletion (`AWS S3`) with pre-signed request for: Posts, Team Profile, and User Profile.
- Websockets with socket.io v3.
- Team creation, Team Member invitation, and settings for Team and User.
- Opinionated architecture:
  - keeping babel and webpack configurations under the hood,
  - striving to minimize number of configurations,
  - `withAuth` HOC to pass user prop and control user access to pages,
  - HOC extensions `MyApp` and `MyDocument`
  - server-side rendering with `Material-UI`,
  - model-specific components in addition to common components.
- Universally-available environmental variables at runtime.
- Custom logger (configure what _not_ to print in production).
- Useful components for any web app: `ActiveLink`, `Confirm`, `Notifier`, `MenuWithLinks`, and more.
- Analytics with `Google Analytics`.
- Production-ready, scalable architecture:
  - `app` - user-facing web app with Next/Express server, responsible for rendering pages (either client-side or server-side rendered). `app` sends requests via API methods to `api` Express server.
  - `api` - server-only code, Express server, responsible for processing requests for internal and external API infrastructures.
- **Subscriptions with `Stripe`**:
  - subscribe/unsubscribe Team to plan,
  - update card information,
  - verified Stripe webhook for failed payment for subscription.


#### Running `api` locally:

- Before running, create a `.env` file inside the `api` folder with the environmental variables as shown below. These variables are also listed in [`.env.example`](https://github.com/async-labs/saas/blob/master/saas/api/.env.example), which you can use as a template to create your own `.env` file inside the `api` foler.

`api/.env`:

  ```
  # Used in api/server/server.ts
  MONGO_URL_TEST=
  MONGO_URL=
  SESSION_NAME=
  SESSION_SECRET=
  COOKIE_DOMAIN=
  
  # Used in api/server/google.ts
  GOOGLE_CLIENTID=
  GOOGLE_CLIENTSECRET=
  
  # Used in api/server/aws-s3.ts and api/server/aws-ses.ts
  AWS_REGION=
  AWS_ACCESSKEYID=
  AWS_SECRETACCESSKEY=
  
  # Used in api/server/models/Invitation.ts and api/server/models/User.ts
  EMAIL_SUPPORT_FROM_ADDRESS=
  
  # Used in api/server/mailchimp.ts
  MAILCHIMP_API_KEY=
  MAILCHIMP_REGION=
  MAILCHIMP_SAAS_ALL_LIST_ID=
  
  ----------
  # All env variables above this line are needed for successful user signup
  
  # Used in api/server/stripe.ts
  STRIPE_TEST_SECRETKEY=sk_test_xxxxxx
  STRIPE_LIVE_SECRETKEY=sk_live_xxxxxx
  
  STRIPE_TEST_PLANID=plan_xxxxxx
  STRIPE_LIVE_PLANID=plan_xxxxxx
  
  STRIPE_LIVE_ENDPOINTSECRET=whsec_xxxxxx
  
  # Optionally determine the URL
  URL_APP="http://localhost:3000"
  URL_API="http://localhost:8000"
  PRODUCTION_URL_APP="https://saas-app.async-await.com"
  PRODUCTION_URL_API="https://saas-api.async-await.com"
  ```
  
  - Your `.env` file file _must_ have values for the `required` variables. To use all features and third-party integrations, also add the `optional` variables.

  - IMPORTANT: do not publish your actual values for environmentable variables in `.env.example`; this file is public and only meant to show you how your `.env` should look.<br/>
  
  - IMPORTANT: use your values for `PRODUCTION_URL_APP` and `PRODUCTION_URL_API`. These are values for domain name that you own.

  - IMPORTANT: The above environmental variables are available on the server only. You should add your `.env` file to `.gitignore` inside the `api` folder so that your secret keys are not stored on a remote Github repo.

  - To get value for `MONGO_URL_TEST`, we recommend you use a [free MongoDB at MongoDB Atlas](https://docs.atlas.mongodb.com/) or [$15/month MongoDB at Digital Ocean](https://www.digitalocean.com/products/managed-databases-mongodb/)
  - Specify your own name and secret keys for Express session: [SESSION_NAME](https://github.com/expressjs/session#name) and [SESSION_SECRET](https://github.com/expressjs/session#express)
  - Get `GOOGLE_CLIENTID` and `GOOGLE_CLIENTSECRET` by following the [official OAuth tutorial](https://developers.google.com/identity/sign-in/web/sign-in#before_you_begin). <br/>
    Important: For Google OAuth app, callback URL is: http://localhost:8000/oauth2callback <br/>
    Important: You have to enable Google+ API in your Google Cloud Platform account.

- Once `.env` is created, you can run the `api` app. Navigate to the `api` folder, run `yarn install` to add all packages, then run the command below:
  ```
  yarn dev
  ```


#### Running `app` locally:

- Navigate to the `app` folder, run `yarn` to add all packages, then run `yarn dev` and navigate to `http://localhost:3000`:

  - A `.env` file in the `app` folder is not required to run, but you can create one to override the default variables. The environmental variables for `.env` in the `app` folder are shown below. You can also refer [`.env.example`](https://github.com/async-labs/saas/blob/master/saas/app/.env.example) for creating your own `.env` file in the `app` folder.<br/>

  ```
    NEXT_PUBLIC_STRIPE_TEST_PUBLISHABLEKEY="pk_test_xxxxxxxxxxxxxxx"
    NEXT_PUBLIC_STRIPE_LIVE_PUBLISHABLEKEY="pk_live_xxxxxxxxxxxxxxx"
    
    NEXT_PUBLIC_BUCKET_FOR_POSTS=
    NEXT_PUBLIC_BUCKET_FOR_TEAM_AVATARS=
    NEXT_PUBLIC_BUCKET_FOR_TEAM_LOGOS=
    
    NEXT_PUBLIC_URL_APP="http://localhost:3000"
    NEXT_PUBLIC_URL_API="http://localhost:8000"
    NEXT_PUBLIC_PRODUCTION_URL_APP=
    NEXT_PUBLIC_PRODUCTION_URL_API=
    
    NEXT_PUBLIC_API_GATEWAY_ENDPOINT=
    NEXT_PUBLIC_GA_MEASUREMENT_ID=
  ```

  - IMPORTANT: do not publish your actual values for environmentable variables in `.env.example`; this file is public and only meant to show you how your `.env` should look.<br/>
  
  - IMPORTANT: use your values for `PRODUCTION_URL_APP` and `PRODUCTION_URL_API`. These are values for domain name that you own.

  - To get `NEXT_PUBLIC_GA_MEASUREMENT_ID`, set up Google Analytics and follow [these instructions](https://support.google.com/analytics/answer/1008080?hl=en) to find your tracking ID.
  - To get `NEXT_PUBLIC_STRIPE_TEST_PUBLISHABLEKEY`, go to your Stripe dashboard, click `Developers`, then click `API keys`.

- For successful file uploading, make sure your buckets have proper CORS configuration. Go to your AWS account, find your bucket, go to `Permissions > CORS configuration`, add:

```
[
  {
    "AllowedHeaders":[
      "*"
    ],
    "AllowedMethods":[
      "PUT",
      "POST",
      "GET",
      "HEAD",
      "DELETE"
    ],
    "AllowedOrigins":[
      "http://localhost:3000",
      "https://saas-app.async-await.com"
    ],
    "ExposeHeaders":[
      "ETag",
      "x-amz-meta-custom-header"
    ]
  }
]
```

- Make sure to update allowed origin with your actual values for `NEXT_PUBLIC_URL_APP` and `NEXT_PUBLIC_PRODUCTION_URL_APP`.

- Once `.env` is created, you can run the `app` app. Navigate to the `app` folder, run `yarn install` to add all packages, then run the command below:
  ```
  yarn dev
  ```


#### Symlink `api` in `lambda`:

In lambda directory we are symlinking api directory. You can run symlink command in lambda folder as mentioned below:
```
bash symlink ../api
```

## Deploy to Heroku, AWS Elastic Beanstalk, API Gateway and AWS Lambda

We give detailed instructions inside Chapter 9 and 10 of our SaaS Boilerplate book: https://builderbook.org/book

## Built with

- [React](https://github.com/facebook/react)
- [Material-UI](https://github.com/mui-org/material-ui)
- [Next](https://github.com/vercel/next.js)
- [MobX](https://github.com/mobxjs/mobx)
- [Express](https://github.com/expressjs/express)
- [Mongoose](https://github.com/Automattic/mongoose)
- [MongoDB](https://github.com/mongodb/mongo)
- [Typescript](https://github.com/Microsoft/TypeScript)

For more detail, check `package.json` files in both `app` and `api` folders and project's root.

To customize styles, check [this guide](https://github.com/async-labs/builderbook#add-your-own-styles).


## Screenshots

Google or passwordless login:
![1_SaaS_login](https://user-images.githubusercontent.com/26158226/61417504-2760b000-a8ac-11e9-8ce6-14fc5947dad0.png)

Dropdown menu for settings:
![2_SaaS_DropdownMenu](https://user-images.githubusercontent.com/26158226/61417505-27f94680-a8ac-11e9-9390-35e17e1626c3.png)

Personal settings:
![3_SaaS_PersonalSettings](https://user-images.githubusercontent.com/26158226/61417514-2891dd00-a8ac-11e9-97d4-53944fe8f897.png)

Team settings:
![4_SaaS_TeamSettings](https://user-images.githubusercontent.com/26158226/61417515-2891dd00-a8ac-11e9-9c08-0d1adef43c5b.png)

Creating a Discussion:
![5_SaaS_Discussion_Creation](https://user-images.githubusercontent.com/26158226/61417509-27f94680-a8ac-11e9-889b-19f96b159d21.png)

Writing a Post, Markdown vs. HTML view:
![6_SaaS_Discussion_Markdown](https://user-images.githubusercontent.com/26158226/61417508-27f94680-a8ac-11e9-93fd-766014132e8d.png)

![7_SaaS_Discussion_HTML](https://user-images.githubusercontent.com/26158226/61417507-27f94680-a8ac-11e9-8058-d3701ef1696d.png)

Discussion between team members:
![8_SaaS_Discussion_Dark](https://user-images.githubusercontent.com/26158226/61417506-27f94680-a8ac-11e9-9cba-cc47ba3b51a8.png)

Billing settings:
![9_SaaS_Billing](https://user-images.githubusercontent.com/26158226/61417513-2891dd00-a8ac-11e9-9e3d-bcbcdfe5b5af.png)

Purchasing a subscription:
![10_SaaS_BuySubscription](https://user-images.githubusercontent.com/26158226/103588107-6407d900-4e9d-11eb-9159-e85301205739.png)

Payment history:
![12_SaaS_PaymentHistory](https://user-images.githubusercontent.com/26158226/61417510-27f94680-a8ac-11e9-88d1-1eef120dcc34.png)


## Contributing

Want to support this project? Consider buying our [books](https://builderbook.org/).


## Team

- [Kelly Burke](https://github.com/klyburke)
- [Timur Zhiyentayev](https://github.com/tima101)

You can contact us at team@async-labs.com.

If you are interested in working with us, check out [Async Labs](https://async-labs.com/).


## License

All code in this repository is provided under the [MIT License](https://github.com/async-labs/saas/blob/master/LICENSE.md).

## Project structure

```
├── .elasticbeanstalk
│   └── config.yml
├── .github
│   └── FUNDING.yml
├── .vscode
│   ├── extensions.json
│   ├── launch.json
│   └── settings.json
├── api
│   ├── .elasticbeanstalk
│   │   └── config.yml
│   ├── server
│   │   ├── api
│   │   │   ├── index.ts
│   │   │   ├── public.ts
│   │   │   ├── team-leader.ts
│   │   │   └── team-member.ts
│   │   ├── models
│   │   │   ├── Discussion.ts
│   │   │   ├── EmailTemplate.ts
│   │   │   ├── Invitation.ts
│   │   │   ├── Post.ts
│   │   │   ├── Team.ts
│   │   │   └── User.ts
│   │   ├── utils
│   │   │   ├── slugify.ts
│   │   │   └── sum.ts
│   │   ├── aws-s3.ts
│   │   ├── aws-ses.ts
│   │   ├── google-auth.ts
│   │   ├── logger.ts
│   │   ├── mailchimp.ts
│   │   ├── passwordless-auth.ts
│   │   ├── passwordless-token-mongostore.ts
│   │   ├── server.ts
│   │   ├── sockets.ts
│   │   └── stripe.ts
│   ├── static
│   │   └── robots.txt
│   ├── test/server/utils
│   │   ├── slugify.test.ts
│   │   └── sum.test.ts
│   ├── .eslintignore
│   ├── .eslintrc.js
│   ├── .gitignore
│   ├── package.json
│   ├── tsconfig.json
│   ├── tsconfig.server.json
│   └── yarn.lock
├── app
│   ├── .elasticbeanstalk
│   │   └── config.yml
│   ├── components
│   │   ├── common
│   │   │   ├── Confirmer.tsx
│   │   │   ├── LoginButton.tsx
│   │   │   ├── MemberChooser.tsx
│   │   │   ├── MenuWithLinks.tsx
│   │   │   ├── MenuWithMenuItems.tsx
│   │   │   └── Notifier.tsx
│   │   ├── discussions
│   │   │   ├── CreateDiscussionForm.tsx
│   │   │   ├── DiscussionActionMenu.tsx
│   │   │   ├── DiscussionList.tsx
│   │   │   ├── DiscussionListItem.tsx
│   │   │   └── EditDiscussionForm.tsx
│   │   ├── layout
│   │   │   ├── index.tsx
│   │   ├── posts
│   │   │   ├── PostContent.tsx
│   │   │   ├── PostDetail.tsx
│   │   │   ├── PostEditor.tsx
│   │   │   └── PostForm.tsx
│   │   ├── teams
│   │   │   └── InviteMember.tsx
│   ├── lib
│   │   ├── api
│   │   │   ├── makeQueryString.ts
│   │   │   ├── public.ts
│   │   │   ├── sendRequestAndGetResponse.ts
│   │   │   ├── team-leader.ts
│   │   │   └── team-member.ts
│   │   ├── store
│   │   │   ├── discussion.ts
│   │   │   ├── index.ts
│   │   │   ├── invitation.ts
│   │   │   ├── post.ts
│   │   │   ├── team.ts
│   │   │   └── user.ts
│   │   ├── confirm.ts
│   │   ├── isMobile.ts
│   │   ├── notify.ts
│   │   ├── resizeImage.ts
│   │   ├── sharedStyles.ts
│   │   ├── theme.ts
│   │   └── withAuth.tsx
│   ├── pages
│   │   ├── _app.tsx
│   │   ├── _document.tsx
│   │   ├── billing.tsx
│   │   ├── create-team.tsx
│   │   ├── discussion.tsx
│   │   ├── invitation.tsx
│   │   ├── login-cached.tsx
│   │   ├── login.tsx
│   │   ├── team-settings.tsx
│   │   └── your-settings.tsx
│   ├── public
│   │   └── pepe.jpg
│   ├── server
│   │   ├── robots.txt
│   │   ├── routesWithCache.ts
│   │   ├── server.ts
│   │   └── setupSitemapAndRobots.ts
│   ├── .babelrc
│   ├── .eslintignore
│   ├── .eslintrc.js
│   ├── .gitignore
│   ├── next.env.d.ts
│   ├── next.config.js
│   ├── package.json
│   ├── tsconfig.json
│   ├── tsconfig.server.json
│   └── yarn.lock
├── book
├── lambda
│   ├── .estlintignore
│   ├── .eslintrc.js
│   ├── .gitignore
│   ├── api
│   ├── handler.ts
│   ├── package.json
│   ├── serverless.yml
│   ├── tsconfig.json
│   └── yarn.lock
├── .gitignore
├── LICENSE.md
├── README.md
├── package.json
├── yarn.lock
```
