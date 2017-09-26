Narrativ Publisher Tag
====================================

Functionality
------------

The Narrativ publisher tag does two main things. First, it will find any SmartLinks on the page and run
the auctions, allowing the destination of the links to be updated ahead of time. Second, it will track user behavior
such as SmartLink impressions and clicks.

Implementation
------------

Getting the publisher tag to run successfully is a simple process. Copy and paste the following Javascript snippet
in the HEAD section of all your site's pages.

* Make sure to replace "ACCOUNT NAME" with your Narrativ account name.
* Need to know your Narrativ account name? Log into dashboard.narrativ.com and go to `setup`_ to see the snippet
  customized with your account info, or reach out to your account manager for support as needed.
* See if it's working: There is a checker on your "setup" page where you can insert your site URL to verify if
  the Narrativ Publisher tag is correctly installed.

::

    <script type="text/javascript">
        (function(window, document, account) {
            window.skimlinks_exclude = ["shop-links.co", "shop-edits.co"];
            var b = document.createElement("script");
            b.type = "text/javascript";
            b.src = "//static.narrativ.com/tags/" + account + ".js";
            b.async = true;
            var a = document.getElementsByTagName("script")[0];
            a.parentNode.insertBefore(b,a);
        })(window, document, "ACCOUNT NAME");
    </script>


.. _setup: https://dashboard.narrativ.com/#/publisher/account/setup
