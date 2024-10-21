# tsearch.org API Endpoints
Documentation for the tsearch.org API

## Corpus
Each document is indexed as part of a corpus, which is the core resource in the API. 

Queries for a given corpus take the following form:

```
tsearch.org/c/{corpus}
```

For example, for the Federal Register:

```
tsearch.org/c/fedreg
```
## Endpoints 
### Search Results

A `corpus` is searched using the endpoint

```
/c/{corpus}/search
```

Using `fedreg` again as an example:
```
/c/fedreg/search?q=President
```
#### Query Parameters
Each search uses the following query parameters:
- `q`: the search term
- `page` (optional): the page of results to view

#### Response Payload
##### Example
Below is an example API response:

```json
{
  "page": 1,
  "pages": 3,
  "resultsCount": 45,
  "results": [
    {
		"reference": "89 FR 84113",
		"url": "https://www.federalregister.gov/d/2024-24300",
		"description": "Notice of Public Briefing of the Utah Advisory Committee to the U.S. Commission on Civil Rights",
		"excerpt": "... an example excerpt..."
		// excerpt may or may not be present
    },
    {
	    "reference": "89 FR 84124",
		"url": "https://www.federalregister.gov/d/2024-24291",
	    "description": "Finding of No Significant Impact and Final Environmental Assessment for DARPA's Reefense Program, Baker Point, Florida"
      // no excerpt
    }
    // more results
  ],
  "links": {
    "first": "/c/fedreg/search?q=President&page=1",
    "last": "/c/fedreg/search?q=President&page=3",
    "next": "/c/fedreg/search?q=President&page=2",
    "previous": null
  }
}
```

##### Response Schema
A query may return many results, and so the API is paginated.

A response's properties are:
- `page`: page number of this response
- `pages`: total number of pages for the query
- `resultsCount`: total number of results
- `results`: an array of results (see below)
- `links`: pagination links to follow for `first`, `last`, `next`, and `previous` pages. Any of these links may be `null`.
##### Results Schema
- `reference`: unique string that identifies the result. This may be a document ID, or something more specific (if it's identifying a paragraph, sentence, or word, for example). A reference is "meaningful" within the context of the corpus: `89 FR 84113` is a document citation in the Federal Register
- `url` : a URL to the source of the match
- `description`: a human-readable string describing the context of the result. It may be a document's title, and could include additional context like section or page number.
- `excerpt` (optional): if available, an excerpt of the original source of the matching document. It may or may not be present

## Table of Contents
In Progress

ⓒ Simpatico Computing LLC, 2024
