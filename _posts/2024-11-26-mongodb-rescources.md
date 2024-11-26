---
layout: post
title: "MongoDB Resources"
excerpt: "MongoDB Resources"
comments: true
categories:
  - .Net
tags: 
  - .net
  - mongodb
---


# MongoDB Resources

## MongoDB with ElasticSearch

- [Indexing MongoDB with ElasticSearch](https://medium.com/@xoor/indexing-mongodb-with-elasticsearch-2c428b676343)
- [5 Different ways to synchronize data from MongoDB to ElasticSearch](https://code.likeagirl.io/5-different-ways-to-synchronize-data-from-mongodb-to-elasticsearch-d8456b83d44f)

## MongoDB in K8s

- [Running a MongoDB Database in Kubernetes with StatefulSets](https://codelabs.developers.google.com/codelabs/cloud-mongodb-statefulset/index.html?index=..%2F..index#0)
- [Resize Storage for One Database Resource](https://docs.mongodb.com/kubernetes-operator/master/tutorial/resize-pv-storage/)
- [Resizing Persistent Volumes using Kubernetes](https://kubernetes.io/blog/2018/07/12/resizing-persistent-volumes-using-kubernetes/)
- [**Resizing StatefulSet Persistent Volumes with zero downtime**](https://itnext.io/resizing-statefulset-persistent-volumes-with-zero-downtime-916ebc65b1d4)
- [Azure PVC resizing](https://gloriapalmagonzalez.medium.com/azure-pvc-resizing-1525a9f97a37)
- [Upgrade MongoDB 4.4](https://docs.mongodb.com/manual/release-notes/4.4-upgrade-standalone/)
- [Upgrade a Replica Set to 4.4](https://docs.mongodb.com/manual/release-notes/4.4-upgrade-replica-set/#std-label-4.4-upgrade-replica-set)
- [Release Notes for MongoDB 5.0](https://docs.mongodb.com/manual/release-notes/5.0/)
- [Backup and Restore MongoDB](https://docs.bitnami.com/tutorials/backup-restore-data-mongodb-kubernetes/)
- [Kubernetes Cron Job To Backup Mongodb Replica Set.](https://medium.com/@shashwatmahar12/kubernetes-install-mongodb-from-helm-cron-job-to-backup-mongodb-replica-set-5fd8df51fe93)
- [Learn how to recreate an existing PVC in a new namespace, reusing the same PV with no data losses](https://webera.blog/recreate-an-existing-pvc-in-a-new-namespace-but-reusing-the-same-pv-without-data-loss-2c7326c0035a)

## MongoDB Enterprise

- [MongoDB Pricing](https://www.mongodb.com/pricing?tck=docs_atlas)
- [MongoDB Enterprise Kubernetes Operator](https://github.com/mongodb/mongodb-enterprise-kubernetes)
- [Install the MongoDB Enterprise Kubernetes Operator](https://docs.mongodb.com/kubernetes-operator/master/tutorial/install-k8s-operator/)
- [MongoDB Enterprise Kubernetes Operator Helm Installation Settings](https://docs.mongodb.com/kubernetes-operator/master/reference/helm-operator-settings/)
- [Getting started with MongoDB Enterprise Operator for Kubernetes](https://medium.com/hackernoon/getting-started-with-mongodb-enterprise-operator-for-kubernetes-bb5d5205fe02)
- [Ops Manager](https://www.mongodb.com/try/download/ops-manager)
- [Plan your MongoDB Enterprise Kubernetes Operator Installation](https://www.mongodb.com/docs/kubernetes-operator/master/tutorial/plan-k8s-operator-install/)

## MongoDB Percona

- [Data at Rest Encryption](https://www.percona.com/doc/percona-server-for-mongodb/LATEST/data_at_rest_encryption.html#local-key-management-using-a-keyfile)
- [WiredTiger Encryption at Rest with Percona Server for MongoDB](https://www.percona.com/blog/2018/11/01/wiredtiger-encryption-at-rest-percona-server-for-mongodb/)
- [Installing Percona Server for MongoDB on Debian and Ubuntu](https://www.percona.com/doc/percona-server-for-mongodb/LATEST/install/apt.html#installing-from-percona-repositories)

## Mongodb Alternatives

1. Cassandra - Unknown integration with elasticsearch (slower reads than writes)
1. RavenDb - High Performant, better encryption
1. CouchDB

### Articles

- https://ravendb.net/articles/choosing-the-best-nosql-database

## Mongo Migration

- [Mongo Migration Documentation](https://github.com/SRoddis/Mongo.Migration)
- [Handling Schema Changes in C# and MongoDB](https://thegreatco.com/posts/20180821/)
- [Working with MongoDB Transactions with C# and the .NET Framework](https://developer.mongodb.com/how-to/transactions-c-dotnet)
- [Handling Schema Changes](https://mongodb.github.io/mongo-csharp-driver/2.10/reference/bson/mapping/schema_changes/)

## Mongo Views

- [Taking a Look at MongoDB Views](https://dzone.com/articles/taking-a-look-at-mongodb-views)
- [db.createView()](https://docs.mongodb.com/manual/reference/method/db.createView/)
- [MongoDB Database Views](https://outofmemoryexception.wordpress.com/2017/10/22/mongodb-database-views/)

## Mongo GridFS

- [GridFS Docs](https://mongodb.github.io/mongo-csharp-driver/2.1/reference/gridfs/gettingstarted/)

##  Mongo Docs

- [Unwind](https://chsakell.gitbook.io/mongodb-csharp-docs/aggregation/bucket-stage)
- [Left Join in MongoDB using the C# driver and LINQ](https://www.niceonecode.com/blog/64/left-join-in-mongodb-using-the-csharp-driver-and-linq)
- [Pagination in MongoDB and the Bucket Pattern](https://dev.to/tariqabughofa/pagination-in-mongodb-and-the-bucket-pattern-k3m)
- [Fast Paging with MongoDB](https://scalegrid.io/blog/fast-paging-with-mongodb/)
- [ParallelScan](https://mongodb.github.io/mongo-csharp-driver/1.11/driver/#parallelscan)
- [KMS Providers](https://www.mongodb.com/docs/manual/core/queryable-encryption/fundamentals/kms-providers/#std-label-qe-reference-kms-providers-azure)
- [MongoDB Code Generations From SQL to MongoDB](https://www.mongodb.com/docs/relational-migrator/code-generation/)

## Mongo Optimizations

- [Monitor and Improve Slow Queries](https://docs.atlas.mongodb.com/performance-advisor/)
- [A few show tricks to find slow queries in mongodb](https://gist.github.com/rantav/3433277)
- [Paging with the Bucket Pattern - Part 2](https://www.mongodb.com/blog/post/paging-with-the-bucket-pattern--part-2)
- [Troubleshooting MongoDB 100% CPU load and slow queries](https://medium.com/mongodb-cowboys/troubleshooting-mongodb-100-cpu-load-and-slow-queries-da622c6e1339)
- [Explain Results](https://docs.mongodb.com/manual/reference/explain-results/)
- [Query Optimization](https://docs.mongodb.com/v4.2/core/query-optimization/#query-selectivity)
- [Measure Index Use](https://docs.mongodb.com/manual/tutorial/measure-index-use/)
- [How to Improve MongoDB Performance](https://enlear.academy/how-to-improve-mongodb-performance-3630b7087031)
- [Optimize Query Performance](https://docs.mongodb.com/manual/tutorial/optimize-query-performance-with-indexes-and-projections/)
- [Performance Best Practices: Indexing](https://www.mongodb.com/blog/post/performance-best-practices-indexing)
- [Understanding indexing and cardinality for MongoDB](https://bharatkalluri.com/posts/cardinality-and-indexing-mongodb)
- [mongodb.countDocuments is slow when result set is large even if index is used](https://stackoverflow.com/questions/57801753/mongodb-countdocuments-is-slow-when-result-set-is-large-even-if-index-is-used)
- [MongoDb sum query](https://stackoverflow.com/questions/18969916/mongodb-sum-query)
- [Making the Most of Monitoring MongoDB](https://www.mongodb.com/blog/post/making-the-most-of-monitoring-mongodb?tck=free_monitoring_read3)
- [Building with Patterns: A Summary](https://www.mongodb.com/blog/post/building-with-patterns-a-summary)
- [Introducing mtools](https://www.mongodb.com/blog/post/introducing-mtools)
- [MTOOLS - A MUST HAVE FOR MONGODB](https://blog.eleven-labs.com/en/mtools-le-pour-mongodb/)
- [Create Queries that Ensure Selectivity](https://www.mongodb.com/docs/manual/tutorial/create-queries-that-ensure-selectivity/)
- [Partial Indexes](https://www.mongodb.com/docs/manual/core/index-partial/)
- [Case Insensitive Indexes](https://www.mongodb.com/docs/manual/core/index-case-insensitive/)
- [Sparse Indexes](https://www.mongodb.com/docs/manual/core/index-sparse/)
- [Compound Indexes](https://www.mongodb.com/docs/manual/core/index-compound/)
- [Aggregation Pipeline Optimization](https://www.mongodb.com/docs/manual/core/aggregation-pipeline-optimization/)
- [Wildcard Indexes](https://www.mongodb.com/docs/manual/core/index-wildcard/)
- [How to Speed-Up MongoDB Regex Queries by a Factor of up-to 10](https://medium.com/statuscode/how-to-speed-up-mongodb-regex-queries-by-a-factor-of-up-to-10-73995435c606)
- [MongoDB Regex, Index & Performance](https://scalegrid.io/blog/mongodb-regular-expressions-indexes-performance/)
- [Multikey Indexes](https://www.mongodb.com/docs/manual/core/index-multikey/)
- [MongoDB SQL ‘Like’ Query Examples using C#](https://www.thecodebuzz.com/mongodb-csharp-driver-like-query-examples/)
- [**The ESR (Equality, Sort, Range) Rule**](https://www.mongodb.com/docs/manual/tutorial/equality-sort-range-rule/)
- [MongoDB Limits and Thresholds](https://www.mongodb.com/docs/manual/reference/limits/#namespaces)

## Mongo Upgrade

- [Upgrade a Standalone to 5.0](https://www.mongodb.com/docs/manual/release-notes/5.0-upgrade-standalone/)

## Mongodb Helm chart

- [MongoDB Helm Chart Documentation](https://github.com/helm/charts/tree/master/stable/mongodb#replication)
- [MongoDB Helm Chart Default Values](https://github.com/helm/charts/blob/master/stable/mongodb/values.yaml)
- [How To Scale a Node.js Application with MongoDB on Kubernetes Using Helm](https://www.digitalocean.com/community/tutorials/how-to-scale-a-node-js-application-with-mongodb-on-kubernetes-using-helm#step-2-%E2%80%94-creating-secrets-for-the-mongodb-replica-set)

## MongoDB Multi Tenancy

- [JohnKnoop.MongoRepository](https://github.com/johnknoop/MongoRepository#multi-tenancy)
- [Building Multi-tenant (SaaS) Applications in .NET Core with Database per Tenant](https://medium.com/@codeprefect/multitenant-application-with-database-per-tenant-87eb33c05ac5)  
- [Multi-tenant ASP.NET Core 2 - Implementing database based tenant provider](https://www.codingame.com/playgrounds/5440/multi-tenant-asp-net-core-2---implementing-database-based-tenant-provider)
- [Implementing tenant providers on ASP.NET Core](https://gunnarpeipman.com/aspnet-core-tenant-providers/)

## MongoDB Sharding

- [MongoDB Sharding](https://docs.mongodb.com/manual/sharding/)
- [MongoDB Sharding: Step by Step Tutorial with Example](https://www.guru99.com/mongodb-sharding-implementation.html)
- [MongoDB - Replication and Sharding Tutorial
](https://www.simplilearn.com/replication-and-sharding-mongodb-tutorial-video)

### Choose MongoDb Sharding Key

- [Sharding](http://learnmongodbthehardway.com/schema/sharding/)
- [MongoDB Sharding: Sharding clusters and choosing the right shard key [Tutorial]](https://hub.packtpub.com/mongodb-sharding-clusters-choosing-right-shard-key/)
- [On Selecting a Shard Key for MongoDB](https://www.mongodb.com/blog/post/on-selecting-a-shard-key-for-mongodb)
- [Refining Shard Keys in MongoDB 4.4 and Above](https://www.percona.com/blog/refining-shard-keys-in-mongodb-4-4-and-above/)

## MongoDB Database Watcher

- [Change Streams](https://docs.mongodb.com/manual/changeStreams/)
- [Open a Change Stream](https://docs.mongodb.com/manual/reference/method/db.collection.watch/#open-a-change-stream)
- [Real Time Data Streaming with MongoDB Change Streams](https://severalnines.com/database-blog/real-time-data-streaming-mongodb-change-streams)
- [Change Streams - MongoDB Docs](https://mongodb.github.io/mongo-csharp-driver/2.9/reference/driver/change_streams/)

## MongoDB Profiler

- [Database Profiler](https://docs.mongodb.com/manual/tutorial/manage-the-database-profiler/)
- [How to Troubleshoot Slow Queries in MongoDB](https://www.netdata.cloud/academy/how-to-troubleshoot-slow-queries-in-mongodb/)
- [Analyze Query Performance](https://www.mongodb.com/docs/manual/tutorial/evaluate-operation-performance/)
- [Interpret Explain Plan Results](https://www.mongodb.com/docs/manual/tutorial/analyze-query-plan/)