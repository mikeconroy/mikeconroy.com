Turn into a series of posts? https://engineering.chrobinson.com/how-to/linking-a-series-of-jekyll-posts/
  Add that this is an ongoing series of posts touching different parts of the topic and the post will continuously be update - feedback is welcome.
  Part 1 - Introduction to ELK & MuleSoft - Why it's used?
  Part 2 - Sending Logs to ELK with Log4j2
    Confirm this works from CloudHub (may be difficult without Logstash being publicly accessible) and disabling CloudHub Logs?? CloudHub appender?
    Log Levels - Do debug logs go through? Errors?
  Part 3 - Sending Logs to ELK with Beats
  Part 4 - Parsing the logs to load cleanly into Elasticsearch
    Index configuration on Elastic Search (should multiple apps go across multiple indexes or a single one).
    Review log4j2 layout - is json layout correct? JSON Parse Error?
    Parsing the elements of the message.
    Correlation ID? Metrics?
  Part 5 - Creating useful dashboards in Kibana to visualise your API.
  Miscellaneous - Format of logs? JSON Layout in Log4j? Log Levels (are Debug sent?). Log4j Properties for different environments.


Other blog posts
  Configuration of Kibana
    Dashboards that could be created??

  logstash -f config/logstash-mule.conf
  ./kibana
  ./mule start
  ./elasticsearch start