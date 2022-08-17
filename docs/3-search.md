---
title: "Search"
slug: "search"
id: "search"
---

## Guidelines:

The search endpoint deals with operations that help you discover the correct information from your objects. The search endpoint comes in variants which are accessed through `/search/{variant name}`.

Search variants all have a request and response type and they are not all the same so it is important to check your requests and also your response handler. Using the [Typescript SDK](https://github.com/operandinc/typescript-sdk) will make things a lot easier.

## Search Variants Reference

### Contents:

`POST: /search/contents`

```tsx
type req = {
  parentIds?: string[];
  query: string;
  max?: number;
  filter?: any;
};

type res = {
  id: string;
  latencyMs: number;
  contents: {
    objectId: string;
    content: string;
  }[];
  objects: {
    [objectId: string]: {
      id: string;
      parentId?: string;
      createdAt: Date;
      updatedAt: Date;
      type: string;
      metadata: any;
      properties: any;
      indexingStatus: string;
      label?: string;
    };
  };
};
```

### Related

`POST: /search/related`

```tsx
type req = {
  parentIds?: string[];
  objectId: string;
  max?: number;
  filter?: any;
};

type res = {
  id: string;
  latencyMs: number;
  objects: {
    id: string;
    parentId?: string;
    createdAt: Date;
    updatedAt: Date;
    type: string;
    metadata: any;
    properties: any;
    indexingStatus: string;
    label?: string;
  }[];
```
