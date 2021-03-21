---
title: How to Add a "Share on Facebook" Link to Your Jekyll Posts
date: 2021-03-23 06:34:00 +08:00
categories:
- web design
tags:
- jekyll
- facebook
---

This site is powered by [Jekyll](https://jekyllrb.com) and [GitHub Pages](https://pages.github.com) and they're both awesome. The best part is that they're completely free. I usually prefer to use no-code tools like [Webflow](http://webflow.com) when doing web design work, but for my personal site I thought I'd have fun with it and practice coding.

Now, I wanted to add a "Share on Facebook" link at the end of my posts as a CTA. The problem was that the tutorials I found were outdated. So, I had to find my own solution.

In case you're wondering how I did it, here are the steps you need to take:

## 1. Create a Facebook app.

Go to the [Facebook Developer](https://developers.facebook.com/) portal and click on "Create App".

## 2. Add your domain and Privacy Policy URL in Settings > Basic.

If you don't have a Privacy Policy yet for your website, you can use
[GetTerms](https://getterms.io) for a free generator.

## 3. Copy your Facebook app ID and add it as variable in your `config.yml` file.

        facebook_app_id: 123456789012345

## 4. Asynchronously load the Facebook SDK for JavaScript into your page.

        <script>
        window.fbAsyncInit = function() {
        FB.init({
        appId            : '{{site.facebook_app_id}}',
        autoLogAppEvents : true,
        xfbml            : true,
        version          : 'v10.0'
        });
        };
        </script>
        <script async defer crossorigin="anonymous" src="https://connect.facebook.net/en_US/sdk.js"></script>

## 5. Place the "Share on Facebook" link wherever you want to put it and then trigger a Share dialog.

        <a href="#" id="shareBtn">Share on Facebook</a>
        <script>
        document.getElementById('shareBtn').onclick = function() {
        FB.ui({
        display: 'popup',
        method: 'share',
        href: '{{ site.url }}{{ page.url }}',
        }, function(response){});
        }
        </script>

## 6. Make sure you have Open Graph tags.

Try [this tutorial](https://danaleegibson.com/jekyll-and-facebook-og-images/) for more info.

And that's it! Your readers can now share your posts on Facebook easily.