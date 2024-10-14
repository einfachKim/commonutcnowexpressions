# UTCNow Expression Guide for Power Automate and Logic Apps

## How to Get Started

To make it easier for you to try out these expressions, we’ve provided a file called [`compose_example.json`](https://github.com/einfachKim/commonutcnowexpressions/blob/main/compose_example.json). You can copy and paste the code from this file directly into your **Flow editor** and see the examples in action within a cloud flow. This will allow you to further explore and use them in your own automations.
If the Compose action does not appear in your Clipboard section make sure to press CTRL+V.

![Flow Example](https://imgur.com/LW0055U)

![Flow Example](https://imgur.com/LZM1MzO.png)

## Introduction: Understanding Date and Time Formatting in Power Automate

When working with automation in Power Automate or Azure Logic Apps, dealing with date and time formats is a common requirement. Whether you're processing tasks based on current dates, logging actions with timestamps, or manipulating schedules, it's essential to know how to handle date and time formatting effectively. One of the most widely used standards for representing dates and times is **ISO 8601**.

In this article, we’ll explore how the `utcNow()` expression works in Power Automate and how to use it to format dates and times according to different needs. We’ll also provide a detailed table of commonly used date formats and expressions, along with instructions on calculating the **ISO week number**, both in German and English.

---

## Background: The ISO 8601 Date and Time Standard

The **ISO 8601** standard defines an internationally accepted way to represent dates and times. It provides a framework for representing times based on UTC (Coordinated Universal Time) and ensures consistency in handling time across different systems and time zones.

The ISO 8601 format is particularly useful in automation workflows, such as Power Automate, because it is unambiguous and helps systems to interpret dates and times consistently regardless of location or language.

### Examples of ISO 8601 date formats:
- Full date and time (with timezone): `2024-10-14T13:45:30Z`
- Date only: `2024-10-14`
- Time only: `13:45:30`

Power Automate supports ISO 8601 date formats by using the `utcNow()` function, which allows you to generate the current date and time in UTC and format it according to your specific needs.

---

## Working with the `utcNow()` Expression in Power Automate

The `utcNow()` function in Power Automate is used to get the current date and time in **UTC** format. You can customize how the date and time are displayed by passing a **format string** to the function. The format string defines how the output will appear—whether as a date, time, or a combination of both.

### Basic usage of `utcNow()`:
- `utcNow()` — Returns the current date and time in UTC.
- `utcNow('yyyy-MM-dd')` — Returns the current date in ISO 8601 format.
- `utcNow('HH:mm:ss')` — Returns the current time.

Additionally, Power Automate allows for more advanced date and time manipulations, such as calculating the current week of the year. This is especially useful for business logic, scheduling, or logging purposes.

---

## Common Date Formats Using `utcNow()`

Here is a comprehensive list of common date and time formats you can use in Power Automate, along with corresponding expressions for both English and German formats.

| Format                         | Expression                                    | Output (Example)          |
|---------------------------------|------------------------------------------------|---------------------------|
| **Month (Numeric)**             | `@{utcNow('MM')}`                             | `10`                      |
| **Year (Full)**                 | `@{utcNow('yyyy')}`                           | `2024`                    |
| **Short Year**                  | `@{utcNow('yy')}`                             | `24`                      |
| **Month Full Name (English)**   | `@{utcNow('MMMM')}`                           | `October`                 |
| **Month Short Name (English)**  | `@{utcNow('MMM')}`                            | `Oct`                     |
| **German Date Format**          | `@{utcNow('dd.MM.yyyy')}`                     | `14.10.2024`              |
| **German Short Date Format**    | `@{utcNow('dd.MM.yy')}`                       | `14.10.24`                |
| **German Date with Month Text** | `@{utcNow('dd. MMM yyyy')}`                   | `14. Okt 2024`            |
| **Full Date with Day (German)** | `@{utcNow('dddd, dd MMMM yyyy')}`             | `Montag, 14 Oktober 2024` |
| **ISO 8601 Date**               | `@{utcNow('yyyy-MM-dd')}`                     | `2024-10-14`              |
| **Date with Slashes (English)** | `@{utcNow('yyyy/MM/dd')}`                     | `2024/10/14`              |
| **Time with Seconds**           | `@{utcNow('HH:mm:ss')}`                       | `13:45:30`                |
| **Time without Seconds**        | `@{utcNow('HH:mm')}`                          | `13:45`                   |
| **Time with Milliseconds**      | `@{utcNow('HH:mm:ss.fff')}`                   | `13:45:30.123`            |
| **ISO 8601 DateTime**           | `@{utcNow('yyyy-MM-ddTHH:mm:ss')}`            | `2024-10-14T13:45:30`     |
| **ISO DateTime with Timezone**  | `@{utcNow('yyyy-MM-ddTHH:mm:ssZ')}`           | `2024-10-14T13:45:30Z`    |
| **DateTime with Space**         | `@{utcNow('yyyy-MM-dd HH:mm:ss')}`            | `2024-10-14 13:45:30`     |
| **German DateTime Format**      | `@{utcNow('dd.MM.yyyy HH:mm:ss')}`            | `14.10.2024 13:45:30`     |
| **German Short DateTime Format**| `@{utcNow('dd.MM.yyyy HH:mm')}`               | `14.10.2024 13:45`        |
| **Compact Date (MMddyyyy)**     | `@{utcNow('MMddyyyy')}`                       | `10142024`                |
| **Compact DateTime (yyyyMMdd)** | `@{utcNow('yyyyMMdd')}`                       | `20241014`                |
| **Unix Timestamp**              | `@{ticks(utcNow())}`                          | `1697294730`              |
| **RFC1123**                     | `@{utcNow('r')}`                              | `Mon, 14 Oct 2024 13:45:30 GMT` |
| **ISO 8601 Long Format**        | `@{utcNow('O')}`                              | `2024-10-14T13:45:30.1234567Z` |
| **Universal Sortable DateTime** | `@{utcNow('u')}`                              | `2024-10-14 13:45:30Z`    |
| **ISO Week Number Calculation** | `@{div(add(dayofyear(addDays(subtractFromTime(utcNow(), if(equals(dayofweek(utcNow()), 0), 6, sub(dayofweek(utcNow()), 1)), 'Day'), 3)), 6), 7)}` | `42` |

---

## Calculating the ISO Week Number in Power Automate

In some use cases, knowing the **ISO week number** (the week of the year) is crucial. Power Automate does not directly support the ISO week number through the `utcNow()` expression, but you can calculate it using a custom formula.

The following expression calculates the correct ISO week number:

```json
@{div(add(dayofyear(addDays(subtractFromTime(utcNow(), if(equals(dayofweek(utcNow()), 0), 6, sub(dayofweek(utcNow()), 1)), 'Day'), 3)), 6), 7)}
