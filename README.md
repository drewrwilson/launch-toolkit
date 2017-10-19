# Toolkit for Launching a New Project

## Step-by-step guide & some code to quickly make a landing page for your new project

This is a checklist and set of tools for quickly launching a new project. After doing this, your project has a simple website, with an embedded signup form for a mailing list, free webhosting, forces HTTPS, and optional links to your social media accounts.


## Background
I start a bunch of projects. Open source software projects, community groups, activist projects, events, all kinds of stuff. Whether it's the beginning a big project or if it's just a one-off quick thing, I usually want to make a simple webpage with a mailing list signup. I find myself doing this frequently enough that I made this toolkit with some code and some notes to help myself very quickly put a project online.

## Goals


## Tools we'll be using

 * _github_ - this code in this github project is a simple webpage. And we'll be using Github Pages, a way that github offers free webhosting.
 * _MailChimp_ - email list management software. free for lists under 2000 signups.
 * _NameCheap_ - a company that allows us to register a domain name. About $10/year for a domain.
 * _Cloudflare_ - A company that allows us to easily enable HTTPS for the webpage for free. Free


### Github

_Goal:_ Fork this repo and begin customizing your webpage and setting up other web services.

 1. Click the fork button at the top of this github project, this will make a copy of this project on your github account.
 1. Add details about your project to `config.yml`. Change the `title`, `tagline`, `description`, `url`.
 1. Add a logo
  1. Upload a logo and overwrite `logo.png` in the `images` directory in this project. The best is a PNG file with a transparent background. You can upload a file by clicking on the `images` folder in this github project and then dragging your logo to that folder.
  1. If you overwrite the existing `logo.png` file then you don't need to do anything further. If your logo has a different filename, you then need to edit `config.yml` and change the line that says `logo: /images/logo.png` to `logo: /images/YOURFILENAME`.
 1. Add your domain to the `CNAME` file. Open up `CNAME` and replace `example.com` with your domain name (don't include http, https or www in the domain name eg just put `yourdomain.com`)
 1. (Optional) Add a privacy policy
  1. Edit `privacy.md` to add your privacy policy for anyone who signs up for your email list.
  1. To display the privacy policy, edit `config.yml` and change the line that says `showPrivacyPolicy: false` to `showPrivacyPolicy: true`.

### MailChimp

_Goal:_ Get form submission URL for email list sign up and spam checker code. Add them to the `config.yml` file in this github project.

  1. Create a new MailChimp account.
  1. Login and go to your email list. Find the option for Signup Forms setup a new account and get the code for a signup link:
  [](toolkit-images/mailchimp-signup-forms.png)
  1. Choose embeddable forms.
  1. Then choose "Super slim form"
  1. Scroll down to find the HTML code.
  1. Find `form action=` copy the URL from there and then open `config.yml` file in this github project and paste that URL to the `mailchimpURI` value.
  1. You need to copy one more thing from the HTML code, it prevents spam submissions to your email list. There should be a line that says 'real people should not fill this in and expect good things - do not remove this or risk form bot signups'. Look for the next `input` tag after that line, there's an attribute in that tag called `name=` and then some garbled text. Copy that garbled text and paste it into the `mailchimpAntiSpamCode` value.

### NameCheap

_Goal:_ Buy a domain and point the nameservers to Cloudflare.

1. Go to NameCheap.com and buy a domain for the project.
1. After paying, go to your Domains dashboard and change the Nameserver settings to custom:
[](toolkit-images/namecheap-custom-nameserver.png)
1. Set the first one to: `cortney.ns.cloudflare.com` and the second one to: `gabe.ns.cloudflare.com`

## Social media
_Goal:_ Add social media links to your webpage.

If you have social media accounts for your project, you can enable social media links on your site by adding the usernames to the appropriate variables in `config.yml`. eg if you have a twitter account, you can add your username to `config.yml` by adding editing the twitter line to say `twitter: drewSaysGoVeg` or for instagram: `instagram: yourinstgramname`. For facebook, some new pages don't yet have a short name. For facebook social media links to work, you need put everything that comes after facebook.com, eg `facebook: theleagueofjust.us` or `facebook: \213213112423\YourFacebookPageName`.

## Optional tools to set up later

 * IFTTT - use this to automate posting across social media platforms. eg Whenever you post to instagram, also post the content to twitter.
 * Google Apps for Nonprofits - if this is a nonprofit or educational project, google apps is a free resource that provides you with a free custom version of gmail, google docs, google calendar and all the other google apps services for organizations.
