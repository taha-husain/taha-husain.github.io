---
title: "UTC Datepicker"
date: 2021-09-19T19:14:25+05:30
draft: true
categories: ["React", "React Datepicker"]
tags: ["react", "react-datepicker", "datepicker", "timezone"]
---

```
  import React from 'react';
  import DatePicker from 'react-datepicker';
  import PropTypes from 'prop-types';

  const UTCDatePicker = ({
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
  }

  UTCDatePicker.propTypes = {
    onChange: PropTypes.func.isRequired
  };

  export default UTCDatePicker;

```
