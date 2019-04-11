Generate Exclusive ClickMate links
==================================

Overview
--------

By providing us a payload with certain product descriptors,
we can return a set of monetizable `ClickMate`_,
along with our point-in-time estimate of the CPC for
each product in the result set.

Your account must be a member of our LinkMate program to use this feature.
For more information about this program, feel free to `contact us`_.


Request
^^^^^^^

::

   GET /api/v1/product_match/clickmate/exclusive_links/


.. list-table::
   :widths: 10 10 80
   :header-rows: 1

   * - Query Param
     - Type
     - Description

   * - publisher_slug
     - string(64)
     - The slug provided by your Narrativ account rep. *Required* Without this we will not know what account to monetize clicks for

   * - gtin
     - string(50)
     - Product descriptor: the GTIN of the product to be wrapped in a ClickMate Link. *Optional, but one product descriptor must be present*

   * - sku
     - string(50)
     - Product descriptor: the SKU of the product to be wrapped in a ClickMate link. *Optional, but one product descriptor must be present*

   * - product_url
     - string(2048)
     - Product descriptor: the URL of the product to be wrapped in a ClickMate link (must be URL encoded!). *Optional, but one product descriptor must be present*

   * - article_url
     - string(2048)
     - The URL of the article your link is coming from (must be URL encoded!). *Optional*

   * - article_name
     - string(100)
     - The name or title of the article your link is coming from. *Optional* We require either this or `aritcle_url` (or both) to correctly group and monetize links




Response
^^^^^^^^




The response data consists of the list ``data``, with each entry
having the following structure:

.. list-table::
   :widths: 10 10 60
   :header-rows: 1

   * - Field Name
     - Type
     - Description

   * - best_effort_cpc
     - string
     - Point in time prediction of the CPC for the merchant publisher pairing.

   * - product_url
     - string
     - The `ClickMate`_ URL which monetizes the retrieved product.


   * - product_information
     - json
     - Retrieved product details
        - brand
            - string
            - The retrieved product's brand

        - gtin
            - string
            - The retrieved product's GTIN

        - image_url
            - string
            - The retrieved product's image URL

        - min_stock
            - boolean
            - If the product is currently in stock or not

        - price
            - string
            - The price of the retrieved product

        - product_name
            - string
            - The retrieved product's name





URL Encoding
------------

All parameters must be URL encoded. See `URL Encoder`_.


Example Requests
----------------

::

    GET /api/v1/exclusive_clickmate_links?publisher_slug=myacct&gtin=77777777777

    GET /api/v1/exclusive_clickmate_links?publisher_slug=myacct&sku=00000000&&gtin=88888888888888

    GET /api/v1/exclusive_clickmate_links?publisher_slug=myacct&sku=00000000&&gtin=99999999999999&product_url=https%3A%2F%2Fwww.merchant.example%2Fproduct%2F123%0A


Example Response
----------------

::

    {
        "data": [
        {
            "product_information": {
                "price": "15.99",
                "product_name": "Example Product",
                "in_stock": true,
                "gtin": "55555555555555",
                "image_url": "https://merchant.example/path/to/image_url",
                "brand": "Example Brand"
            },
            "clickmate_link": "https://shop-links.co/link/?url=https%3A%2F%2Fwww.merchant.example%2Fproduct%2F123%0Aexclusive=1&publisher_slug=myacct",
            "best_effort_cpc": 0.50
            }
        ]
    }


.. _contact us: mailto:hello@narrativ.com
.. _URL Encoder: https://www.urlencoder.org/
.. _ClickMate: http://docs.narrativ.com/en/stable/clickmate.html
