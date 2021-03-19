---
title: How to Add a "Share on Facebook" Link to Your Jekyll Posts
date: 2021-03-23 06:34:00 +08:00
categories:
- web design
---

This site runs on GitHub Pages and Jekyll and because they're awesome. The best part is that they're completely free. I usually prefer to use no-code tools when doing web design work, but for my personal site I thought I'd have fun with it and practice coding.

Now, I wanted to add a "Share on Facebook" link at the end of my posts as a CTA. The problem was that the tutorials I found were outdated. So, in the hopes that a beginner developer would be helped by this, here are the steps you need to take:

1. Create a Facebook app.

   Go to

2. Add your domain and Privacy Policy page.

3. Copy your Facebook app ID and add it to your config.yml file, like so:

4. Put the following code wherever you want to place the "Share on Facebook" link.

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

5. Make sure you have Open Graph tags.

And that's it! Your readers can now share your posts on Facebook easily.

Note that