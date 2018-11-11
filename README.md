# grok_handbook
My hope is that this will become the go-to handbook for all grok needs

# What is Grok?

## What are Regular Expressions?

Regular Expressions, or sometimes called regex/regexp, is a "string-/pattern-matching language" for use with pieces of text.  
The beauty of it shines with large or even massive text-files (both as in massive singular files or as in massive amount of files) and it's capabilities to find strings/patterns of your choice.
It is however, not always the most easy thing to read, especially for someone who've never even tried writing one before.


# What are Grok patterns?

Grok patterns are in essence just regular expresssions split into parts of the pattern made easy to read with human readable names instead of "weird" syntax that you would have to interpret.
You can even create a grok pattern by combining multiple pre-existing grok patterns (it's in fact very common to do so).
But why would you even want to combine them? Why not just make an entirely new one?   
  
The simple answer is that it's a lot easier to read a pattern written in human readable names, plus you gain the ability to reuse the individual parts for other patterns later.  
Take this example:

```yaml
filter {
    grok {
            match => { "message" => "%{COMMONAPACHELOG}" }
    }
}
```

`%{COMMONAPACHELOG}` is a commonly used Grok pattern that actually consists of multiple grok patterns.
It's definition is as follows:  

`COMMONAPACHELOG %{IPORHOST:clientip} %{HTTPDUSER:ident} %{USER:auth} \[%{HTTPDATE:timestamp}\] "(?:%{WORD:verb} %{NOTSPACE:request}(?: HTTP/%{NUMBER:httpversion})?|%{DATA:rawrequest})" %{NUMBER:response} (?:%{NUMBER:bytes}|-)`  
  
But how would this look if it printed out as a regular expression instead?  
(I honestly began doing it for the entire string but gave up long before halfway, so the example below is just for **IPORHOST**)

```perl
((((([0-9A-Fa-f]{1,4}:){7}([0-9A-Fa-f]{1,4}|:))|(([0-9A-Fa-f]{1,4}:){6}(:[0-9A-Fa-f]{1,4}|((25[0-5]|2[0-4]\d|1\d\d|[1-9]?\d)(\.(25[0-5]|2[0-4]\d|1\d\d|[1-9]?\d)){3})|:))|(([0-9A-Fa-f]{1,4}:){5}(((:[0-9A-Fa-f]{1,4}){1,2})|:((25[0-5]|2[0-4]\d|1\d\d|[1-9]?\d)(\.(25[0-5]|2[0-4]\d|1\d\d|[1-9]?\d)){3})|:))|(([0-9A-Fa-f]{1,4}:){4}(((:[0-9A-Fa-f]{1,4}){1,3})|((:[0-9A-Fa-f]{1,4})?:((25[0-5]|2[0-4]\d|1\d\d|[1-9]?\d)(\.(25[0-5]|2[0-4]\d|1\d\d|[1-9]?\d)){3}))|:))|(([0-9A-Fa-f]{1,4}:){3}(((:[0-9A-Fa-f]{1,4}){1,4})|((:[0-9A-Fa-f]{1,4}){0,2}:((25[0-5]|2[0-4]\d|1\d\d|[1-9]?\d)(\.(25[0-5]|2[0-4]\d|1\d\d|[1-9]?\d)){3}))|:))|(([0-9A-Fa-f]{1,4}:){2}(((:[0-9A-Fa-f]{1,4}){1,5})|((:[0-9A-Fa-f]{1,4}){0,3}:((25[0-5]|2[0-4]\d|1\d\d|[1-9]?\d)(\.(25[0-5]|2[0-4]\d|1\d\d|[1-9]?\d)){3}))|:))|(([0-9A-Fa-f]{1,4}:){1}(((:[0-9A-Fa-f]{1,4}){1,6})|((:[0-9A-Fa-f]{1,4}){0,4}:((25[0-5]|2[0-4]\d|1\d\d|[1-9]?\d)(\.(25[0-5]|2[0-4]\d|1\d\d|[1-9]?\d)){3}))|:))|(:(((:[0-9A-Fa-f]{1,4}){1,7})|((:[0-9A-Fa-f]{1,4}){0,5}:((25[0-5]|2[0-4]\d|1\d\d|[1-9]?\d)(\.(25[0-5]|2[0-4]\d|1\d\d|[1-9]?\d)){3}))|:)))(%.+)?|(?<![0-9])(?:(?:[0-1]?[0-9]{1,2}|2[0-4][0-9]|25[0-5])[.](?:[0-1]?[0-9]{1,2}|2[0-4][0-9]|25[0-5])[.](?:[0-1]?[0-9]{1,2}|2[0-4][0-9]|25[0-5])[.](?:[0-1]?[0-9]{1,2}|2[0-4][0-9]|25[0-5]))(?![0-9]))|\b(?:[0-9A-Za-z][0-9A-Za-z-]{0,62})(?:\.(?:[0-9A-Za-z][0-9A-Za-z-]{0,62}))*(\.?|\b))
```

If you tried scrolling all the way to the right on the example above, you'll realize just how unruly good regular expressions can become if the logs you're parsing have a complex format.
And if you've played with regular expressions, you'll know just how difficult it can be sometimes to write a regular expression that matches **ONLY** what you're looking for, but thanks to the rest of your grok patterns that you've (probably) supplied, it's ok if one grok pattern could match more then what you want since you're only asking it to match a string/pattern before and/or after something else.
The entire string/pattern must match or the pattern isn't considered a match! 

## How to build a Grok-pattern using "default" patterns

## How to create your own Grok-pattern

## Tips for improving Grok-patterns

# Multiline log-handling

**README**  
This part will contain tips that hopefully will be reusable in more systems then just Graylog in combination with Filebeat, but at this point, I can't make any promises. See this part of the guide as examples on how you could handle log-files where one message stretches over multiple lines and adapt to the softwares of your choice.  
I have links to articles discussing Logstash, but since the basics of Logstash and the extraction-functionality in Graylog are more or less the same (at least where it matters for this guide), I will just talk about Graylog and Filebeat for now.

## Using backreferences to match multiple lines

The links below contains tips on how to manage multiline messages and the link about regex-backreferences is for a specific case I'm currently trying to solve at work; how to handle multiline logs where a change in a specific field means it's a new message.

- Filebeat: [Manage multiline messages](https://www.elastic.co/guide/en/beats/filebeat/current/multiline-examples.html)
- Filebeat: [Examples of multiline configuration](https://www.elastic.co/guide/en/beats/filebeat/current/_examples_of_multiline_configuration.html)
- Regex: [Using Backreferences To Match The Same Text Again](https://www.regular-expressions.info/backref.html)

### Use anchor-points!

# Test your Grok-patterns
- [Test grok patterns](http://grokconstructor.appspot.com/do/match)
- [Grok Debugger](https://grokdebug.herokuapp.com/)

# Test Regular Expressions 

- [regular expressions 101](https://regex101.com/)
- [Regular-Expressions.info](https://www.regular-expressions.info/)

# Sources of information

- [Logstash Grok filter plugin](https://www.elastic.co/guide/en/logstash/current/plugins-filters-grok.html)
- [Grok-patterns from Logstash](https://github.com/logstash-plugins/logstash-patterns-core/blob/master/patterns/grok-patterns)

## Multiline messages

- [Manage multiline messages](https://www.elastic.co/guide/en/beats/filebeat/current/multiline-examples.html)
- [Examples of multiline configuration](https://www.elastic.co/guide/en/beats/filebeat/current/_examples_of_multiline_configuration.html) 

## Regex anchor-points and how they solve performance-issues
- [Do you grok?](https://www.elastic.co/blog/do-you-grok-grok)
- [Killing your Logstash performance with Grok](https://medium.com/@momchil.dev/killing-your-logstash-performance-with-grok-f5f23ae47956)
