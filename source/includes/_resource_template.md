# Resource Name

Brief description of the resource.

## The resource object

```json
{
  "id": 1,
  type: "resources",
  // etc
}
```

FIELDS
(aka, attributes that can be requested via ?fields=)

Name | Type | Description
---- | ---- | -----------
id | integer | Unique identifier for the object.
type | string | String representing the object's type. Objects of the same type share the same value.
titled | string | String representing what specific investment vehicle owns this investment.
amount | positive integer | A positive integer representing how much this investment will supply.
created_at | timestamp | Time at which the object was created. Stored in ISO8601, and transmitted in UTC.
completed_on | timestamp | Time at which the investment was completed. Stored in ISO8601, and transmitted in UTC.

## Relationships
aka, relationships that can be requested via ?include

Name | Relationship
---- | ------------
Processes | An investment can have a variety of concurrent processes which need to be fulfilled on it.
Tasks | An investment can have a variety of tasks, through processes.

