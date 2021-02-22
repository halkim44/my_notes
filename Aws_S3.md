# Amazon Simple Storage Service(S3)

## Concepts

### Buckets

a container for objects.

Buckets serve serveral purpose:

- organize the Amazon S3 namespace at the highest level
- identify the account responsible for storage and data transfer charges.
- play a role in access control
- serve as the unit of aggregation for usage reporting.

### Objects

- the fundamental entities stored in Amazon S3.
- consist of object data and metadata.
- uniquely identified within a bucket by a key and a version ID.

### Keys

- unique identifier for an object within a bucket
- Every object in Amazon S3 can be uniquely addressed through the combination of the web service endpoint, bucket name, key, and optionally, a version.

### Regions

- You can choose thee geographical AWS Region where Amazon S3 will store the buckets that you create.
- choose a Region based on latency, costs or address regulatory requirements
- Objects stored in a Region never leave the Region unless you explicitly transfer them to another region.
