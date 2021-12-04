---
title: "React Datepicker - How to select Date and time in UTC"
date: 2021-09-19T11:28:55+05:30
categories: [Tech]
tags: [react, react-datepicker, utc, timezone]
---

By default, [React Datepicker](https://www.npmjs.com/package/react-datepicker)
selects date and time in local timezone.
To select date in a specified timezone
we need to convert timezone manually.
To do so, we may also need to use library like
[Moment Timezone](https://momentjs.com/timezone/).

This blog focuses on selecting date and time in
standard UTC timezone
and its implementation doesn't require
extra library installation.

The original
[implementation](https://github.com/JohnStarich/sage/blob/b422b0ccef05fffe29143f335017ad2fc24f76fc/web/src/UTCDatePicker.js)
is suggested by
[@JohnStarich](https://github.com/JohnStarich).
This implementation has a bit of tweak to accommodate time picker.

```jsx
import React from 'react';
import DatePicker from 'react-datepicker';

export default const UTCDatePicker = ({
  startDate,
  endDate,
  selected,
  onChange,
  ...props
}) => {
  const convertLocalToUTCDate = (localDate) => {
    if (!localDate) return localDate;

    const date = new Date(localDate);
    const utcDate = new Date(
            date.getUTCFullYear(),
            date.getUTCMonth(),
            date.getUTCDate(),
            date.getUTCHours(),
            date.getUTCMinutes(),
          );
    return utcDate;
  }

  const convertUTCToLocalDate = (utcDate) => {
    if (!utcDate) return utcDate;

    const date = new Date(utcDate);
    const localDate = new Date(
            Date.UTC(
              date.getFullYear(),
              date.getMonth(),
              date.getDate(),
              date.getHours(),
              date.getMinutes()
            )
          );
    return localDate;
  }

  return (
    <DatePicker
      startDate={convertLocalToUTCDate(startDate)}
      endDate={convertLocalToUTCDate(endDate)}
      selected={convertLocalToUTCDate(selected)}
      onChange={date => onChange(convertUTCToLocalDate(date))}
      {...props}
    />
  )
};
```

Above example ignores local timezone
while selecting date and time
using datepicker and instead uses
UTC timezone.
