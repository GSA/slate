---
title: API Reference

language_tabs:
  - sh

toc_footers:
  - <a href='http://search.digitalgov.gov'>Sign Up for a Developer Key</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the i14y Content API! You can use our API to publish your CMS documents into our indexes to power your DigitalGov Search box.

By hooking into the existing lifecycle of documents in your CMS, you can create/update/delete the associated documents in our indexes via this Content API.

Ruby/Python/Node clients are welcome.

# Authentication

> To authorize, use this code:

```sh
# With curl, you can just pass the correct header with each request
curl "https://i14y.usa.gov/api/v1/documents"
  -XPOST 
  -u your_collection_handle:your_secret_token 
```

> Make sure to replace `your_collection_handle` with the name you were issued, and make sure you replace `your_secret_token` with the API key you were given.

The i14y API uses keys to allow access to the API. For now, you can request access via [email](mailto:search@support.digitalgov.gov).

The i14y API expects the key to be included in all API requests to the server in a Basic authentication header that looks like the following:

`Authorization: Basic qG9yZW46bG9yZW5pMTR5dG9rZW4=`

<aside class="notice">
You must replace <code>your_collection_handle</code> and <code>your_secret_token</code> with your personal collection handle and API key.
</aside>

# HTTPS

All access to the i14y Content API must use SSL.

# Documents

## Create a document

```sh
curl "https://i14y.usa.gov/api/v1/documents"
  -XPOST 
  -u your_collection_handle:your_secret_token
  -d '{"document_id":"1",
      "title":"this is a fairly short title",
      "path": "http://www.gov.gov/cms/doc1.html", 
      "created": "2015-05-12T22:35:09Z",
      "description":"some more information here on the document", 
      "content":"the long form body of the document", 
      "promote": false, 
      "language" : "en"
      }'
```

> The above command returns JSON structured like this:

```json
{
"status":200,
"developer_message":"OK",
"user_message":"Your document was successfully created."
}
```

This endpoint creates a document.

### HTTP Request

`POST https://i14y.usa.gov/api/v1/documents`

### Query Parameters

Parameter | Required | Description 
--------- | ------- | ----------- 
document_id | true | A document ID that is unique to your CMS.
title | true | Document title.
path | true | Document link URL.
created | true | When document was initially created (e.g., '2013-02-27T10:00:00Z') 
description | false | Document description.
content | false | Document content.
changed | false | When document was modified (e.g., '2013-02-27T10:00:01Z')
promote | false | Whether to promote the document in the relevance ranking
language | false | Two-letter locale describing language of document (defaults to 'en')

<aside class="success">
Remember — you must pass in at least one of description or content, preferably both!
</aside>

## Update a document

```sh
curl "https://i14y.usa.gov/api/v1/documents/{document_id}"
  -XPUT 
  -u your_collection_handle:your_secret_token
  -d '{"title":"check out this info...today only!",
      "promote": true"
      }'
```

> The above command returns JSON structured like this:

```json
{
"status":200,
"developer_message":"OK",
"user_message":"Your document was successfully updated."
}
```

This endpoint updates a document.

### HTTP Request

`PUT https://i14y.usa.gov/api/v1/documents/{document_id}`

### Query Parameters

Parameter | Required | Description 
--------- | ------- | ----------- 
title | false | Document title.
path | false | Document link URL.
created | false | When document was initially created (e.g., '2013-02-27T10:00:00Z') 
description | false | Document description.
content | false | Document content.
changed | false | When document was modified (e.g., '2013-02-27T10:00:01Z')
promote | false | Whether to promote the document in the relevance ranking
language | false | Two-letter locale describing language of document (defaults to 'en')

<aside class="success">
Your updates are reflected in your search results within seconds!
</aside>

## Delete a document

```sh
curl "https://i14y.usa.gov/api/v1/documents/{document_id}"
  -XDELETE 
  -u your_collection_handle:your_secret_token
```

> The above command returns JSON structured like this:

```json
{
"status":200,
"developer_message":"OK",
"user_message":"Your document was successfully deleted."
}
```

This endpoint deletes a document.

### HTTP Request

`DELETE https://i14y.usa.gov/api/v1/documents/{document_id}`

<aside class="success">
Remember- The `document_id` is what you assigned the document when you created it.
</aside>
