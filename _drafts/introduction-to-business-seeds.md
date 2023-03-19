---
layout: post
title: Introduction to Business Seeds
---

Event id should be considered as an opaque identifier. This gurantee that the id is not open for interpretion. This discourages the consumers from building business-logic on top of the event ids. The event ids sole responsibility is to promote and enable idempotent consumers. The consumers are not responsible for interpreting the data of each events to detect duplicates. The prodeucers dictates how duplicated are identified by generating a reproducible and unique event id. The consumer can rely on the event ids to be discard events that is already processed. This is especially important for consumers whom cannot gurantee idempotence.

Unique and reproducible event ids can be difficult to generate without relying on a persistence layer to keep track of all the events produced. One technique that can be applied to gurantee unique and reproducible event ids is to use a business seed. The business seed consist of a set of partial seeds each of represent domain and business data that is available to the producer during runtime. These partial seeds make up the business seed that generate a unqiue and reproducible event id. One way to use the business seed is to convert into into a byte array that can used in generate a UUID. This UUID will represent opaque, unique, and reproducible identifier.

(Why do events ids have to be unique and reproducible?)

Identifying business seeds are a purely analytical process. Business seeds depend on the domain knowledge and what data that is available during runtime. Business seeds cannot be solved solely by libratization.

Timestamps should be carefully considered before using them as partial seeds for the business seed. Here are a few scenarios where timestamps might be a good candidate for a business seed. 
- The event describes an action that happened based on a user submission and the event is expeted to be produced regardless if all the data  within the event is identical to previously produced events.
- The timestamp can be used as a business seed if the producer can gurantee that the timestamp remains identical across several application instances (E.g. due to application restarts). Timestamps that are generated at runtime each time that the event is produced is not a good candidate for the business seed. This can yield duplicated events that are meant to be identical but with different event ids.


Event IDs should be considered as opaque identifiers. This guarantees that the ID is not open for interpretation. This discourages consumers from building business logic on top of the event IDs. The event ID's sole responsibility is to promote and enable idempotent consumers. The consumers are not responsible for interpreting the data of each event to detect duplicates. The producers dictate how duplicates are identified by generating a reproducible and unique event ID. The consumer can rely on the event IDs to discard events that have already been processed. This is especially important for consumers who cannot guarantee idempotence.

Unique and reproducible event IDs can be challenging to generate without relying on a persistence layer to keep track of all the events produced. One technique that can be applied to guarantee unique and reproducible event IDs is to use a business seed. The business seed consists of a set of partial seeds, each representing domain and business data that is available to the producer during runtime. These partial seeds make up the business seed that generates a unique and reproducible event ID. One way to use the business seed is to convert it into a byte array that can be used to generate a UUID. This UUID will represent an opaque, unique, and reproducible identifier.

Event IDs need to be unique and reproducible to ensure that each event is recognized as distinct and can be consistently identified across different instances. This allows for efficient processing and handling of events, making it easier to detect duplicates and maintain data integrity in the system.

Identifying business seeds is a purely analytical process. Business seeds depend on domain knowledge and the data available during runtime. Business seeds cannot be solved solely by standardization.

Timestamps should be carefully considered before using them as partial seeds for the business seed. Here are a few scenarios where timestamps might be a good candidate for a business seed:

The event describes an action that happened based on a user submission, and the event is expected to be produced regardless of whether all the data within the event is identical to previously produced events.
The timestamp can be used as a business seed if the producer can guarantee that the timestamp remains identical across several application instances (e.g., due to application restarts). Timestamps that are generated at runtime each time the event is produced are not good candidates for the business seed. This can yield duplicate events that are meant to be identical but have different event IDs, leading to potential confusion and data inconsistencies.