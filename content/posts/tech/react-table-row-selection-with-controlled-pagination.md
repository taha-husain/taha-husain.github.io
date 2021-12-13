---
title: "React Table - How to implement row selection with controlled server-side pagination"
date: 2021-10-22T15:12:17+05:30
draft: true
categories: [React, React Table]
tags: [react, react-table]
---

In this blog,
we will implement
multi-row selection
and select all
with controlled
server-side pagination
in React
using React Table hooks.

We will use
examples provided by
`react-table` for
[controlled pagination](https://react-table.tanstack.com/docs/examples/pagination-controlled)
and
[row selection and pagination](https://react-table.tanstack.com/docs/examples/row-selection-and-pagination)
and work our way to acheive desired result.

### Implementation

#### Step 1
To select all rows,
we would need unique identifier
of all rows pre-fetched
on the page.
Pass all ids to the `Table` component.

#### Step 2
Use `getToggleAllRowsSelectedProps`
instead of `getToggleAllPageRowsSelectedProps`
for header checkbox
to trigger rows select event across
all pages.
Note - `getToggleAllRowsSelectedProps` works
seamlessly for frontend pagination,
but needs to be customized for
server-side pagination.

#### Step 3
Set `autoResetSelectedRows` table option to `false`.

#### Step 4
Add following custom `stateReducer` as a table option.

*Definition*
```js
const extractSelectedRowIds = (ids) =>
  ids.reduce((row, id) => ({ ...row, [id]: true }), {});

const stateReducer = (ids) => (newState, action) => {
  if (action.type === "toggleAllRowsSelected") {
    // determine if the header checkbox is selected or deselected
    // if selected then push all ids into selectedRowIds
    if (action.value) {
      return {
        ...newState,
        selectedRowIds: extractSelectedRowIds(ids)
      };
    }
    // else empty selectedRowIds state
    return { ...newState, selectedRowIds: {} };
  }
  return newState;
};
```

*`useTable` options*
```js
useTable(
  {
    columns,
    data,
    ...
    autoResetSelectedRows: false,
    getRowId: (row) => row.id,
    stateReducer: stateReducer(ids)
  },
  ...
)
```
Note: `ids` is an array of
unique identifiers of complete dataset.

After setting above custom table options,
the header checkbox will select
all rows instead of page rows,
and selected rows will remain
selected even after page change
or navigation.

### Downside
While implementing
these customizations,
it's only fair to discuss
downside of this approach.
When we have huge data,
say in thousands or even more,
above approach is not recommended
because it can slow down the
selection and de-selection process
on the page.

### Conclusion
In this blog,
we implemented
*Select All* checkbox
with controlled pagination
and discussed its pitfalls.

For complete code of above implementation,
please check out following codesandbox.


{{< rawhtml >}}
  <iframe src="https://codesandbox.io/embed/react-table-row-selection-with-server-side-pagination-ygv0s?fontsize=14&hidenavigation=1&theme=dark"
    style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
    title="react-table-row-selection-with-server-side-pagination"
    allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
    sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
  ></iframe>
{{< /rawhtml >}}
