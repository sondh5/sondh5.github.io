---
layout: post
title:  "[Shopify App] Open any link in new tab"
excerpt: "You can't not open link in new tab with stacks: Rails, Turbolinks, React Polaris"
author: sondh5
categories: [ Rails, React, Shopify ]
image_hidden: true
featured: false
status: public
---

Recently I moved to a new world - Shopify, working on some apps with tech stack: Rails, Turbolinks, React.
I am using React Polaris component library to quickly create the best experience for Shopify merchants.

<hr>

I got 2 problems (or just my merchant need):
- Page reload
- Open link in new tab

#### Page reload
`RoutePropagator` lets you synchronize a Shopify embedded app's URL with the parent page.

```react
<AppBridgeProvider config={config}>
  <AppBridgeRouterSync />
  [...]
</AppBridgeProvider>
```

```react
// app/javascript/components/AppBridgeRouterSync.js
import React from "react";
import { withRouter } from "react-router-dom";
import { RoutePropagator } from "@shopify/app-bridge-react";

const AppBridgeRouterSync = ({ location }) => {
  return <RoutePropagator location={location} />;
};

export default withRouter(AppBridgeRouterSync);
```

#### Open link in new tab
> Polaris doesn't have it documented

> If you pass an HTML element in your Index.Row that has "data-primary-link", it'll change the behaviour of the click event to navigate instead.

```react
<IndexTable.Row>
  <IndexTable.Cell>
    <a
      href={`your path`}
      data-primary-link
      className="Polaris-Link Polaris-Link--monochrome Polaris-Link--removeUnderline"
    >
      Your value
    </a>
  </IndexTable.Cell>
</IndexTable.Row>

```
*References*
- https://shopify.dev/apps/tools/app-bridge/react-components/route-propagator
- https://community.shopify.com/c/shopify-discussions/clickable-row-in-index-table-polaris/td-p/1506114
