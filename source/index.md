---
title: i14y API Instructions

language_tabs:
  - sh: cURL

toc_footers:
  - <a href='mailto:search@support.digitalgov.gov'>Email us for an i14y API key</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# What is i14y?

Our i14y API allows you to send content directly from your content management system (CMS) into [DigitalGov Search](http://search.digitalgov.gov/) for real-time indexing. By hooking into your CMS workflow, you can immediately [create](#create-a-document), [update](#update-a-document), and [delete](#delete-a-document) the associated documents in our search indexes via this API.

Even if you don’t have a CMS, you can develop software to publish your content in a way that meets the i14y API specifications below.

Ruby/Python/Node clients are welcome.

Using i14y is optional. The rest of our service offering will continue as-is, providing the default web results from commercial indexes.

## What are the main benefits of i14y?

By a long shot, the two features we get asked for most are:

1. Immediate inclusion of new or updated content in search results.
2. Control over which documents are (or are not) in your search index.

i14y answers both of these requests.

# Authentication

You'll need to have a [DigitalGov Search account](https://search.usa.gov/sites) and at least one site already set up.

> To authorize, use this code:

```sh
# With curl, you can just pass the correct header with each request
curl "https://i14y.usa.gov/api/v1/documents"
  -XPOST 
  -u your_collection_handle:your_secret_token 
```

> Replace `your_collection_handle` with the your collection handle, and replace `your_secret_token` with your API key.

The i14y API uses keys to allow access to the API. While we're still in beta, [email us](mailto:search@support.digitalgov.gov) to request access.

The i14y API expects the key to be included in all API requests to the server in a Basic authentication header that looks like the following:

`Authorization: Basic qG9yZW46bG9yZW5pMTR5dG9rZW4=`

<aside class="notice">
Replace <code>your_collection_handle</code> with your collection handle, and replace <code>your_secret_token</code> with your API key.
</aside>

# Create, update, and delete documents

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

You must use https.

### Query Parameters

Parameter | Required | Description 
--------- | ------- | ----------- 
document_id | true | A document ID that is unique to your CMS
title | true | Document title
path | true | Document link URL
created | true | When the document was initially created (such as '2013-02-27T10:00:00Z') 
description | false* | Document description
content | false* | Document content
changed | false | When document was modified (such as '2013-02-27T10:00:01Z')
promote | false | Whether to promote the document in the relevance ranking
language | false | Two-letter [locale](https://github.com/GSA/punchcard/tree/master/localizations) describing language of document (defaults to 'en')

<aside class="success">
* You must pass either a description or content, and preferably both!
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

You must use https.

### Query Parameters

Parameter | Required | Description 
--------- | ------- | ----------- 
title | false | Document title
path | false | Document link URL
created | false | When document was initially created (such as '2013-02-27T10:00:00Z') 
description | false | Document description
content | false | Document content
changed | false | When document was modified (such as '2013-02-27T10:00:01Z')
promote | false | Whether to promote the document in the relevance ranking
language | false | Two-letter [locale](https://github.com/GSA/punchcard/tree/master/localizations) describing language of document (defaults to 'en')

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

You must use https.

<aside class="success">
The `document_id` is the ID you assigned to the document when you created it.
</aside>
