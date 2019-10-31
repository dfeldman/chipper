# chipper

# thesis
elasticsearch is the main log storage DB out there now, but it requires a bunch of big servers with reliable storage, so it isn't a good fit for cloud native environments with tons of transient containers

# design
ingest in fluentd forward protocol (https://github.com/fluent/fluentd/wiki/Forward-Protocol-Specification-v1), since fluentd already has plugins for everything

cluster logs by source application and respond to any currently running queries/rules, then store in compressed & encrypted chunks of a few hundred MB

upload logs to object store (minio?)

offline indexer goes through objects and creates indexes using BLEVE, then uploads them to object store as well

queries hit the index objects
