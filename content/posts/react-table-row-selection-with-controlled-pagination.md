---
title: "React Table - How to implement row selection with controlled server-side pagination"
date: 2021-10-22T15:12:17+05:30
draft: true
categories: [React, React Table]
tags: [react, react-table]
---

In this blog,
we will try to explain
how to implement
multi-row selection
and select all
with controlled
server-side pagination.

We will use
examples provided by `react-table` for
[controlled pagination](https://react-table.tanstack.com/docs/examples/pagination-controlled)
and
[row selection and pagination](https://react-table.tanstack.com/docs/examples/row-selection-and-pagination)
and work our way to acheive desired result.


{{< rawhtml >}}
  <iframe src="https://codesandbox.io/embed/react-table-row-selection-with-server-side-pagination-ygv0s?fontsize=14&hidenavigation=1&theme=dark"
    style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
    title="react-table-row-selection-with-server-side-pagination"
    allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
    sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
  ></iframe>
{{< /rawhtml >}}
