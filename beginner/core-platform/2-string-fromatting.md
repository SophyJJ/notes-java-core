# String formatting

- StringBuilder and String concatenation are not strong enough. Need better ones.

## StringJoiner

```java
// delimiter, start, and end
StringJoiner sj = new StringJoiner(", ", "{", "}");
sj.add("these");
sj.add("words").add("are").add("split");
sj.add("by");
sj.add("commas");
String result = sj.toString();
// {these, words, are, split, by, commas}
// very easy to do: [this], [vaues], [in], [brackets]
// you can also set empty values
```

## String.format

- it takes format specifiers:
  - % [argument index][flags][width][precision] conversion-type
- conversion-type
  - d= decimal - integral
  - f= decimal - floating
  - s= string <= calls formattable. If not specified, then calls toString()
- you can do padding, padding with 0s, justify, format number with commas, show +/- sign
- more information in Java Formatter documentation
