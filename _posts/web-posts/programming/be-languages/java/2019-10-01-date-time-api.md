---
layout: post
title: Java8 Date Time API
date:   2019-10-01 07:25:00 +0100
categories: [backend, java, java8]
tags: [programming, backend, java, java8]
---
The main improvements over previous classes are Thread safety and ease of use.  

## LocalDate  
Represents a date in ISO format (yyyy-MM-dd) **without time**.

~~~ java
// Declaration
final LocalDate ld1 = LocalDate.now();
final LocalDate ld2 = LocalDate.of(2015, 02, 20);
final LocalDate ld3 = LocalDate.parse("2015-02-20");
~~~

<!--more-->

~~~ java
// Add and substract units  
final LocalDate today = LocalDate.now();
final LocalDate tomorrow = today.plusDays(1);
final LocalDate future = today.plus(1, ChronoUnits.CENTURIES);  
final LocalDate past = today.minus(1, ChronoUnits.ERAS);

// Utility methods
final LocalDate now = LocalDate.now();
final DayOfWeek dow = now.getDayOfWeek();
final boolean isLeapYear = now.isLeapYear();

// compare days
final LocalDate yesterday = LocalDate.now().minusDays(1);
final boolean isBefore = yesterday.isBefore(now);
~~~

## LocalTime  
Represents a time, **without date**.

~~~ java
// Declaration
final LocalTime lt1 = LocalTime.now();
final LocalTime lt2 = LocalTime.parse("06:30");
final LocalTime lt3 = LocalTime.of(06, 30);

// Add and substract  
final LocalTime future = LocalTime.now().plusHours(1);

// Utilities
final LocalTime max = LocalTime.MAX;
~~~

## LocalDateTime  
It's a combination of date and time. This is the most commonly used class.

~~~ java
// Declaration
final LocalDateTime ldt1 = LocalDateTime.now();
final LocalDateTime ldt2 = LocalDateTime.of(2015, Month.FEBRUARY, 20, 06, 30);
final LocalDateTime ldt3 = LocalDateTime.parse("2015-02-20T06:30:00");

// It has methods from the previous 2.
final LocalDateTime future1 = ldt1.plusDays(1);
final LocalDateTime future2 = ldt1.plusHours(5);
~~~

## ZonedDateTime & OffsetDateTime
Used when we need to deal with specific time zones. It uses a LocalDateTime + ZoneId for _ZonedDateTime_ or LocalDateTime + ZoneOffset for _OffsetDateTime_.

~~~ java
// ZonedDateTime.
final LocalDateTime now = LocalDateTime.now();
final ZoneId zone = ZoneId.of("Europe/Berlin");
final ZonedDateTime zdt = ZonedDateTime.of(now, zone);

// OffsetDateTime
final ZoneOffset zo = ZoneOffset.of("+02:00");
final OffsetDateTime odt = OffsetDateTime.of(now, zo);
~~~

## Period & Duration
Period represents the time in years, months and days, passed between two **LocalDates**  

~~~ java
final LocalDate now = LocalDate.now();
final LocalDate future = now.plusDays(5);  

final Period period = Period.between(now, future);
final int daysPassed = period.getDays();
~~~

Duration represents the time in seconds and nano-seconds from a **LocalTime**.  

~~~ java
final LocalTime now = LocalTime.now();
final LocalTime past = now.minusMinutes(50);

final Duration dur = Duration.between(now, past);
final int nanos = dur.getNano();
~~~
# Reference(s)
[https://www.baeldung.com/java-8-date-time-intro](https://www.baeldung.com/java-8-date-time-intro)
