---
title: Vendor Review

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Vendor Review API
---
# Introduction

This API request help you retrieve all the vendor's review


  ## Get all reviews from a vendor

list of all the vendors reviews created on your site by calling the WCMp vendors API and using the GET method.

```shell
curl --location --request GET https:///wcmpdemos.com/demo1/wp-json/wcmp/v1/vendors/59/reviews'

  #The above command returns JSON structured like this:

  ```json
  {
    "id": 59,
    "rating_count": 1,
    "avg_rating": "5.0",
    "reviews_list": [
      {
        "id": 376,
        "review_content": "amazing store",
        "review_rating": 5,
        "reviewer_id": "1",
        "reviewer_name": "superadmin",
        "reviewer_email": "abhirup@dualcube.com",
        "reviewer_verified": false,
        "date_created": "2022-03-30T06:47:35",
        "_links": {
          "self": [
            {
              "href": "http://wcmpdemos.com/demo1/wp-json/wcmp/v1/vendors/59/reviews/376"
            }
          ],
          "collection": [
            {
              "href": "http://wcmpdemos.com/demo1/wp-json/wcmp/v1/vendors/59/reviews"
            }
          ],
          "up": [
            {
              "href": "http://wcmpdemos.com/demo1/wp-json/wcmp/v1/vendors/59"
            }
          ]
        }
      }
    ]
  }
  ```
  list of all the vendors reviews created on your site by calling the WCMp vendors API and using the GET method.

  ### HTTP Request

  `GET [site_url]/wp-json/wcmp/v1/vendors/[vendor_id]/reviews`

  ### Query Parameters

  Parameter  | Description
  ---------  | -----------
   vendor_id | Unique identifier for the vendor
   review_id | Unique identifier for a review

  <aside class="success">
  Remember — to add the proper site URL !
  </aside>







