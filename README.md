# Toolkit for Launching a New Project

## Step-by-step guide & some code to quickly make a landing page for your new project

This is a checklist and a small amount of code that makes it easy to for me to quickly launch a new project. After going through step-by-step guide, you'll have a a simple website for your new project with an embedded email list signup form, free webhosting, HTTPS enabled by default, and optional links to any of your social media accounts.

## Background
I start a bunch of projects. Open source software projects, community groups, activist projects, events, all kinds of stuff. I need webpages and email lists for each one. Whether it's a big project or it's just a one-off quick thing, I usually want to make a simple webpage for it with a mailing list signup. I find myself doing this frequently enough that I made this toolkit with some code and some notes to help myself very quickly put a project online.

## Tools we'll be using

 * **github** - this code in this github project is a simple webpage. And we'll be using Github Pages, a way that github offers free webhosting.
 * **MailChimp** - email list management software. free for lists under 2000 signups.
 * **NameCheap** - a company that allows us to register a domain name. About $10/year for a domain.
 * **Cloudflare** - A company that allows us to easily enable HTTPS for the webpage for free. Free

_And now onto the step-by-step guide!_

### Github

**Goal:** Setup a simple customized website with free hosting.

 1. Click the fork button at the top of this github project, this will make a copy of this project on your github account.
 1. Now you should be working on the fork of the project. Rename the github project to the name of the new project that you're launching.
 1. An FYI for experienced developers. Usually your git repository has a `master` branch. In this project, I've added the `gh-pages` branch and deleted the `master` branch. Having a `gh-pages` branch tells github that you want the code in this project to be served via Github Pages, their free webhosting program. And since this only has a webpage, we no longer need the `master` branch. I've found that keeping `master` around only leads to confusion, so I deleted it entirely.
 1. Customize the webpage.
  1. Edit `config.yml` to add the details about the project that you're launching.
    * `title` is the title of your project
    * `tagline` is a very short description of your project. This will go right on the homepage.
    * `description` is a few sentences describing your project. This is used in the social media sharing text.
    * `url` is the explicit URL of your project. Right now you can make it `http://YourGithubUsername.github.io/github-project-name` and this webpage will load fine. If you are buying a domain for your project (covered later), you can go ahead and put your URL here. Or you could always come back after you buy a domain and change this.
 1. Add a logo
  1. Upload a logo and overwrite `logo.png` in the `images` directory in this project. The best is a PNG file with a transparent background. You can upload a file by clicking on the `images` folder in this github project and then dragging your logo to that folder.
  1. If you overwrite the existing `logo.png` file then you don't need to do anything further. If your logo has a different filename, you then need to edit `config.yml` and change the line that says `logo: /images/logo.png` to `logo: /images/YOURFILENAME`.
  1. Optional: You can add a background image for the site. Upload an image to the `images` directory in this github project, just like you did for the logo. Now edit `config.yml` and add the path to your background image, eg `/images/background.jpg`.
  1. Optional: You can also now add a social media sharing image. This is different from your logo because it's the image that facebook and twitter will use as the preview image when someone is sharing a link to your webpage on their social network. If you have a custom one, you can leave it set to the same as your logo (`/images/logo.png`).
 1. Add your domain to the `CNAME` file. Open up `CNAME` and replace `example.com` with your domain name (don't include http, https or www in the domain name eg just put `yourdomain.com`). If you haven't already, go back to `config.yml` and update your `url` in the config file with your domain name.
 1. (Optional) Add a privacy policy
  1. Edit `privacy.md` to add your privacy policy for anyone who signs up for your email list.
  1. To display the privacy policy, edit `config.yml` and change the line that says `showPrivacyPolicy: false` to `showPrivacyPolicy: true`.

### MailChimp

**Goal:** Get form submission URL for email list sign up and spam checker code. Add them to the `config.yml` file in this github project.

  1. Create a new MailChimp account.
  1. Login and go to your email list. Find the option for Signup Forms setup a new account and get the code for a signup link:

  [](toolkit-images/mailchimp-signup-forms.png)

  1. Choose embeddable forms.
  1. Then choose "Super slim form"
  1. Scroll down to find the HTML code.
  1. Find `form action=` copy the URL from there and then open `config.yml` file in this github project and paste that URL to the `mailchimpURI` value.
  1. You need to copy one more thing from the HTML code, it prevents spam submissions to your email list. There should be a line that says 'real people should not fill this in and expect good things - do not remove this or risk form bot signups'. Look for the next `input` tag after that line, there's an attribute in that tag called `name=` and then some garbled text. Copy that garbled text and paste it into the `mailchimpAntiSpamCode` value.

### NameCheap

**Goal:** Buy a domain and point the nameservers to Cloudflare.

1. Go to NameCheap.com and buy a domain for the project.
1. After paying, go to your Domains dashboard and change the Nameserver settings to custom:

[](toolkit-images/namecheap-custom-nameserver.png)

1. Set the first one to: `cortney.ns.cloudflare.com` and the second one to: `gabe.ns.cloudflare.com`

### Cloudflare

**Goal:** Point your new domain to github pages for webhosting and enable HTTPS.

 1. Create an account with Cloudflare and Login.
 1. Add your new domain. It will likely ask to scan your domain for existing DNS entries. Choose a free account.
 1. After you add your new domain, go select it from the dropdown at the top of the page and go to the DNS settings.
 1. Delete all of the existing DNS entries.
 1. Now we're going to setup the domain to point to Github Pages for free webhosting.
  1. Add an A Name entry. Set the Name to `@` and set the Value to `192.30.252.153`.
  1. Add a second A Name entry. Set the Name to `@` and set the Value to `192.30.252.153`.
  1. Add a CNAME entry. Set the Name to `www` and set the value to `YOURDOMAIN.com`. Your DNS setting should look like this:

[](toolkit-images/cloudflare-dns-settings.png)

 1. Now let's enable HTTPS.
  1. Go to the Page Rules tab.
  1. Click 'Create Page Rule' and `http://yourdomain.com/` to the text field and choose 'Always Use HTTPS' from the dropdown settings menu. Click 'Save and Deploy'.
  1. Add another page rule for `http://yourdomain.com/*` and again choose 'Always Use HTTPS'. Save and deploy.
  1. Test HTTPS by loading http://yourdomain.com in your browser. It should automatically redirect you to the https version of the site and a small lock icon should appear in your browser. This means that data is now being encrypted from the browser to your server.



## Social media
*Goal:* Add social media links to your webpage.

If you have social media accounts for your project, you can enable social media links on your site by adding the usernames to the appropriate variables in `config.yml`. eg if you have a twitter account, you can add your username to `config.yml` by adding editing the twitter line to say `twitter: drewSaysGoVeg` or for instagram: `instagram: YourInstgramName`. For facebook, some new pages don't yet have a short name. For facebook social media links to work, you need put everything that comes after facebook.com, eg `facebook: theleagueofjust.us` or `facebook: \213213112423\YourFacebookPageName`.

## Optional tools to set up later

 * IFTTT - use this to automate posting across social media platforms. eg Whenever you post to instagram, also post the content to twitter.
 * Slack notifications - get automatic slack notifications when someone signs up for your email list or takes another kind of action.
 * Google Apps for Nonprofits - if this is a nonprofit or educational project, google apps is a free resource that provides you with a free custom version of gmail, google docs, google calendar and all the other google apps services for organizations.
