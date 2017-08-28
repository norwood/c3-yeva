# C3 demo for tutorial

Bootstrapped from: https://github.com/cjmatta/ConfluentPlatformWikipediaDemo

Repropriating (with changes) for C3 101 Tutorial

# Steps

```bash
docker-compose up -d
```

Then to add the connector:

```bash
HEADER="Content-Type: application/json"
DATA=$( cat << EOF
{
  "name": "wikipedia-irc",
  "config": {
      "producer.interceptor.classes": "io.confluent.monitoring.clients.interceptor.MonitoringProducerInterceptor",
      "connector.class": "org.cmatta.kafka.connect.irc.IrcSourceConnector",
      "irc.server": "irc.wikimedia.org",
      "kafka.topic": "wikipedia.raw",
      "irc.channels": "#en.wikipedia,#en.wiktionary,#en.wikibooks,#en.wikinews,#es.wikipedia,#fr.wikipedia",
      "tasks.max": "2"
  }
}
EOF
)
curl -X POST -H "${HEADER}" --data "${DATA}" http://localhost:8083/connectors
```

How do I add it via the GUI without getting the error

