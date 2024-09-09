# Social network

## Functional requirements

 - User can create post with images and description and connection to a location
    - User can see posts of other users
    - User can comment
    - User can react to a post
 - User can subscribe to other users
 - Search of popular places
   - User can see posts of these places
 - See feeds of other users

## Non-Functional requirements

 - DAU: 10M
 - Availability: 99.99%

[//]: # ( - Latency: 100ms)
 - Clients: Web + App
 - Store all the data
 - Only one region
 - Holiday seasons

### RPS

 - Posts (write)
   - Let's assume 1 post per user per day
     - RPS = 10_000_000 * 1 / 100_000 = 100 r/s
     - CC = 10M / 10 = 1M
     - 1 post = 1MB + 10KB = 1.01MB ~ 1MB
     - Traffic = 10_000_000 r/day * 1 MB * 365 days = 3_650_000_000 MB/year = 365 0000 GB/year = (replication) TB/year = 3.66 PB/year
     - we can use replication x2 to save some space. 7 PB/ year
 - Comments (write)
    - Let's assume 1 comment per user per day
    - RPS = 10_000_000 * 1 / 100_000 = 100 r/s
    - CC: 10M / 10 = 1M
    - 1 comment = 100KB
    - Traffic = 10_000_000 r/d * 0.1MB * 365 = 365_000_000 KB/year = 365 TB/year
    - to store 365 * 3 (replication)
 - Reactions (write)
    - Let's assume 10 reaction per user per day
    - RPS = 10_000_000 * 10 / 100_000 = 1000 r/s
    - CC: 10M / 10 = 1M
    - 1 reaction = 10KB
    - Traffic = 10_000_000 r/day * 10 * 365 days * 10 KB = 365 000 000 000 KB/year = 365 TB/year
    - to store, it wil require less space, 1KB per action - 36 TB/year * 3 (replication)

