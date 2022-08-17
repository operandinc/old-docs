---
title: "Completion"
slug: "completion"
id: "completion"
---

## Guidelines:

The completion endpoint focuses on operations that generate useful information from your objects. The completion endpoint comes in variants which are accessed through `/completion/{variant name}`.

Completion variants all have a request and response type and they are not all the same so it is important to check your requests and also your response handler. Using the [Typescript SDK](https://github.com/operandinc/typescript-sdk) will make things a lot easier.

## Completion Variants Reference

### Answer:

`POST: /completion/answer`

```tsx
type req = {
  parentIds?: string[];
  question: string;
  filter?: any;
};

type res = {
  id: string;
  latencyMs: number;
  answer: string;
  sources: {
    id: string;
    parentId?: string;
    createdAt: Date;
    updatedAt: Date;
    type: string;
    metadata: any;
    properties: any;
    indexingStatus: string;
    label?: string;
  }[]; // Array of objects where information contained in the answer came from.
};
```

### Typeahead

`POST: /completion/typeahead`

```tsx
type req = {
  parentIds?: string[];
  text: string;
  count?: number;
  filter?: any;
};

type res = {
  id: string;
  latencyMs: number;
  completions: string[];
  sources: {
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
