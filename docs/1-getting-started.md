---
title: "Getting Started"
slug: "getting-started"
id: "getting-started"
---

### Introduction:

Welcome to the Operand API! This API is the core of what we offer and it is how we build all of our own products. Any and all feedback is welcome to help improve documentation or the endpoints themselves and can be sent [here](mailto:support@operand.ai) or join our [discord server](https://discord.gg/WpaFpt5C9M) to do all of this and more!

<aside>
💡 The guide is designed for usage with our serverless product.

</aside>

At a high-level Operand provides the infrastructure and API to turn your static knowledge/data/information into dynamic natural language features and our world-class infrastructure enables lightning-fast experiences everywhere.

### Using the API:

**Host:**

The API is accessible at https://prod.operand.ai.

**Format:**

The API a standard REST API, and uses JSON-encoding for both request and response bodies.

**Authorization:**

All requests must include an `Authorization` header with an API key, which will be accessible from your serverless dashboard.

<aside>
⚠️ **At the moment, requests to our API should only be performed server-side** In the future, there will be finer grained permissions for keys (e.g. for client-side operations).

</aside>

**Errors:**

Standard HTTP Errors are provided with descriptive messages and an additional error code for support purposes.

### First Steps:

Start by [creating an account](/auth) which will take you to our serverless dashboard. The serverless dashboard has an object browser and various settings for your account.

The object browser is a thin ui wrapper ontop of the API that lets you explore the basic structure of your objects and provides some functionality for object management (uploading,deleting,etc). Using the object browser is the easiest way to get started without having to write any code!

The settings page lets you configure your account and also has your API key which you will need if you want to do anything outside of the object browser.

<aside>
👉 If you are using Typescript or Go you can use our [Typescript SDK](https://github.com/operandinc/typescript-sdk) or [Go SDK](https://github.com/operandinc/go-sdk) to make your life easier.

</aside>

**Step 0: [Optional] Create a Collection Object**

We highly recommend beginning by creating a Collection Object so that you can keep your project organized. Collections act as folders in our Object tree structure and it will be much easier to maintain and use your project by using them. That said feel free to ignore us but if you make a mess you might have to clean it up.

Dashboard:

1. Use Cmd+K or click the "do stuff" button in the top right.
2. Type "create collection" or select it from the menu.
3. Add a label and then click "create".
4. You should see a new collection in the object browser.

SDK:

```tsx
const col = await operand.createObject({
  type: "collection",
  metadata: {},
});
```

**Step 1: Add Objects**

Assuming you followed our advice you can use your Collection Object’s `id` as the `parentId` parameter when creating objects, if you decided to be naughty you can just leave it empty. Feel free to add any type of object you like we have provided a lovely example below for adding some text as an Object.

Dashboard:

1. Click into the collection object like you would a folder.
2. Use the cmd+k menu again but this time select the "create text" option.
3. Add a label, write something fun, then click "create".
4. You should see a new text object in the object browser.
5. Wait for it to finish indexing!

SDK:

```tsx
const textObj = await operand.createObject({
  type: "text",
  metadata: {
    text: "The FitnessGram PACER Test is a multistage aerobic capacity exam.",
  },
  parent: col.id, // optional
});
```

**Step 2: Perform an Operation**

Now that we have an Object (or maybe more) we can do the fun stuff: Operations. Operations are how you interact with the objects and create the magical experiences for your users. While there are lots of Operation variants we will use `/search` and the variant `contents` allowing us to get content-based semantic search results from our Objects.

Dashboard:

1. Use the search bar next to the object browser.

SDK:

```tsx
const results = await operand.searchContents({
  parentIds: [col.id],
  query: "How to assess fitness?",
  max: 10,
});
```

**Step 3: ????**

**Step 4: Profit**

Go make awesome features and let us know so we can write a case-study!
