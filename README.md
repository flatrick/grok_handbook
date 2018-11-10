# grok_handbook
My hope is that this will become the go-to handbook for all grok needs

# What is Grok?

## What are regex/regexp/Regular Expressions?

# What are grok patterns?

## How to build a Grok-pattern using "default" patterns

## How to create your own Grok-pattern

## Tips for improving Grok-patterns

# Multiline log-handling

**README**  
This part will contain tips that hopefully will be reusable in more systems then just Graylog, but at this point, I can't make any promises. See this part of the guide as examples on how you could handle log-files where one message stretches over multiple lines.


### Use regex anchor-points!

# Test your Grok-patterns
- [Test grok patterns](http://grokconstructor.appspot.com/do/match)
- [Grok Debugger](https://grokdebug.herokuapp.com/)

# Test Regular Expressions 

- [regular expressions 101](https://regex101.com/)
- [Regular-Expressions.info](https://www.regular-expressions.info/)

# Sources of information

- [Logstash Grok filter plugin](https://www.elastic.co/guide/en/logstash/current/plugins-filters-grok.html)
- [Grok-patterns from Logstash](https://github.com/logstash-plugins/logstash-patterns-core/blob/master/patterns/grok-patterns)

## Regex anchor-points and how they solve performance-issues
- [Do you grok?](https://www.elastic.co/blog/do-you-grok-grok)
- [Killing your Logstash performance with Grok](https://medium.com/@momchil.dev/killing-your-logstash-performance-with-grok-f5f23ae47956)
