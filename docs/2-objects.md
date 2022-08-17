---
title: "Objects"
slug: "objects"
id: "objects"
---

## Type Definition:

```tsx
type Object = {
  id: string; // uuid of object
  parentId?: string; // uuid of parent object
  createdAt: timestamp; // timestamp of creation
  updatedAt: timestamp; // timestamp of most recent update
  type: string; // object type. List of objects below
  metadata: {
    // required metadata derived from object type
  };
  properties: {
    // optional user defined properties of object.
    // typically used for filtering during operations.
  };
  indexingStatus: string; // status of object (ready, error, indexing)
  label?: string; // optional label for object
};
```

## General Guidelines:

Objects are the fundamental building block of the Operand API and their design is heavily informed by file systems. In our file system the Collection Object Type is equivalent to the folder while all other Object Types should be treated as files. It is highly recommended you keep your projects organized with Collection Objects.

## API Reference:

### Add a new object

`POST: /v3/objects`

```tsx
type req = {
  parentId?: string;
  type: string;
  metadata: any;
  properties?: any;
  label?: string;
};

type res = {
  id: string;
  parentId?: string;
  createdAt: timestamp;
  updatedAt: timestamp;
  type: string;
  metadata: any;
  properties: any;
  indexingStatus: string;
  label?: string;
};
```

### List objects

`GET: /v3/objects?parentId={parentId}&limit={limit}&startingAfter={startingAfter}&endingBefore={endingBefore}`

```tsx
type urlParams = {
  parentId?: string;
  limit?: number;
  startingAfter?: string;
  endingBefore?: string;
};

type res = {
  objects: {
    id: string;
    parentId?: string;
    createdAt: timestamp;
    updatedAt: timestamp;
    type: string;
    metadata: any;
    properties: any;
    indexingStatus: string;
    label?: string;
  }[];
  hasMore: boolean;
};
```

### Get an object

`GET: /v3/objects/{id}`

```tsx
type urlParams = {
  id: string;
};

type res = {
  id: string;
  parentId?: string;
  createdAt: timestamp;
  updatedAt: timestamp;
  type: string;
  metadata: any;
  properties: any;
  indexingStatus: string;
  label?: string;
};
```

### Update an object

`PUT: /v3/objects/{id}`

```tsx
type urlParams = {
  id: string;
};

type req = {
  type: string;
  metadata: any;
  properties?: any;
};

type res = {
  id: string;
  parentId?: string;
  createdAt: timestamp;
  updatedAt: timestamp;
  type: string;
  metadata: any;
  properties: any;
  indexingStatus: string;
  label?: string;
};
```

### Delete an object

`DELETE: /v3/objects/{id}`

```tsx
type urlParams = {
  id: string;
};

type res = {
  deleted: boolean;
};
```

## Object Type Reference:

### Collection

**Input:** `collection` \
**Description:** A Collection is used to organize your objects in the API. Collections are very flexible and can be used to hold a few objects or a lot. Beyond basic organization, Collections can be used for multi-tenancy and various other hierarchical structures. Collections have an empty metadata object.\
**Metadata:**

```tsx
type metadata = {}; // empty
```

### Text

**Input:** `text` \
**Description:** Text is the most basic and unstructured object we support.\
**Metadata:**

```tsx
type metadata = {
  text: string; // Your text goes here
};
```

### HTML

**Input:** `html` \
**Description:** Stores well structured html. Poorly formatted html will not be as understandable or useful.\
**Metadata:**

```tsx
type metadata = {
  html: string; // Your html goes here
  title?: string; // optional title
};
```

### Markdown

**Input:** `markdown` \
**Description:** Stores the string content of .md files.\
**Metadata:**

```tsx
type metadata = {
	markdown: string // Your markdown goes here
	title?: *string // optional title
}
```

### Epub

**Input:** `epub` \
**Description:** Indexes the text content of an epub file.\
**Metadata:**

```tsx
type metadata = {
  epubUrl: string; // url of epub file
  title?: string; // optional title
  language?: string; // optional language
};
```

### PDF

**Input:** `pdf` \
**Description:** Indexes the text content of a PDF file.\
**Metadata:**

```tsx
type metadata = {
  pdfUrl: string; // url of pdf file
};
```

### Image

**Input:** `image` \
**Description:** Indexes a description of the image and any text in the image. Currently .png and .jpeg are supported formats\
**Metadata:**

```tsx
type metadata = {
  imageUrl: string; // url of a valid image file
};
```

### GitHub Repository

**Input:** `github_repository` \
**Description:** Indexes files within a GitHub repository. Currently only Markdown (.md/.mdx) files are supported.\
**Metadata:**

```tsx
type metadata = {
  accessToken: string; // access token for GitHub API
  repoOwner: string; // owner of the repository
  repoName: string; // name of the repository
  rootPath?: string; // optional root path of files to index. defaults to root of repository.
  rootURL?: string; // optional root url that will be prepended to files to create a full url.
};
```

### Audio

**Input:** `audio` \
**Description:** Indexes audio files. Currently only .wav files are supported.\
**Metadata:**

```tsx
type metadata = {
  audioUrl: string; // url of a valid audio file
};
```

### RSS

**Input:** `rss` \
**Description:** Indexes the RSS feed located at the url.\
**Metadata:**

```tsx
type metadata = {
  rssUrl: string; // url of a valid RSS feed
};
```

### Notion

**Input:** `notion` \
**Description:** Indexes the authorized notion pages.\
**Metadata:**

```tsx
type metadata = {
  accessToken: string; // access token for Notion API
};
```

### MBOX

**Input:** `mbox` \
**Description:** Indexes emails from the .mbox file .\
**Metadata:**

```tsx
type metadata = {
  mboxUrl: string; //  url of an mbox file
};
```
