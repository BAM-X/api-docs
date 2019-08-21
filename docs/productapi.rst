Product API
============

Overview
--------

By providing us a payload with certain product descriptors,
we will return a set of monetizable :ref:`ClickMate <clickmate_overview>`
links, along with our point-in-time estimate of the CPC for
each product in the result set.


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
     - (*Required*) The slug provided by your Narrativ account rep.

   * - gtin
     - string(14)
     - **Product descriptor** (*Optional*): the GTIN of the product to be wrapped in a ClickMate link

   * - sku
     - string(255)
     - **Product descriptor** (*Optional*): the SKU of the product to be wrapped in a ClickMate link

   * - product_url
     - string(2048)
     - **Product descriptor** (*Optional*): the URL of the product to be wrapped in a ClickMate link (must be URL encoded)

   * - article_url
     - string(2048)
     - (*Required*): The URL of the article your link is coming from (must be URL encoded)

   * - article_name
     - string(100)
     - (*Required*): The name or title of the article your link is coming from


Required Parameters
^^^^^^^^^^^^^^^^^^^

- Option 1: Provide at least one **product descriptor** in your API request (``gtin``, ``sku``, ``product_url``) and both ``article_url`` and ``article_name``. 
- Option 2: Provide at least one **product descriptor** in your API request (``gtin``, ``sku``, ``product_url``) but omit both ``article_url`` and ``article_name``. But in this case, append both ``article_url`` and ``article_name`` as query parameters to the resulting ClickMate link.
  See :ref:`the ClickMate documentation <clickmate_overview>` for more information.


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
     - float
     - Point in time prediction of the CPC for the merchant publisher pairing in USD

   * - clickmate_link
     - string
     - The :ref:`ClickMate <clickmate_overview>` URL which monetizes the retrieved product


   * - product_information
     - json
     - Product details
        - brand
            - string
            - The retrieved product's brand

        - gtin
            - string
            - The retrieved product's GTIN

        - image_url
            - string
            - The retrieved product's image URL

        - in_stock
            - boolean
            - If the product is currently in stock or not

        - price
            - string
            - The price of the retrieved product in USD

        - product_name
            - string
            - The retrieved product's name

        - merchant_name
            - string
            - The name of the merchant selling the retrieved product


URL Encoding
------------

All parameters must be URL encoded. See `URL Encoder`_.


Example Requests
----------------

::

    GET /api/v1/product_match/clickmate/exclusive_links/?publisher_slug=myacct&gtin=77777777777

    GET /api/v1/product_match/clickmate/exclusive_links/?publisher_slug=myacct&sku=00000000&&gtin=88888888888888

    GET /api/v1/product_match/clickmate/exclusive_links/?publisher_slug=myacct&sku=00000000&&gtin=99999999999999&product_url=https%3A%2F%2Fwww.merchant.example%2Fproduct%2F123%0A


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
                    "brand": "Example Brand",
                    "merchant_name": "Example Retailer"
                },
                "clickmate_link": "https://shop-links.co/link/?url=https%3A%2F%2Fwww.merchant.example%2Fproduct%2F123%0Aexclusive=1&publisher_slug=myacct",
                "best_effort_cpc": 0.50,
            }
        ]
    }


.. _contact us: mailto:hello@narrativ.com
.. _URL Encoder: https://www.urlencoder.org/
