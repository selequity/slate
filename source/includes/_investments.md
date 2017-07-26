# Investments

Investments are how deals get funded. Each investment can have a variety
of concurrent processes running on it at the same time.

## Attributes
```json
{
  "id": "25",
  "type": "investments",
  "attributes": {
    "user_id": null,
    "deal_id": null,
    "workflow_state": "complete",
    "amount": 0,
    "created_at": "2017-04-12T13:27:18.317Z",
    "updated_at": "2017-04-12T13:27:18.317Z",
    "accredify_token": null,
    "accreditation_id": null,
    "deal_terms": true,
    "documents_understood": true,
    "titled": "Charles George III",
    "completed_on": null,
    "will_be_rejected": null,
    "pre_reject_state": null,
    "fa_investment_id": null,
    "fa_investor_id": null,
    "accreditation_subtype": null,
    "project_id": 4,
    "suitability_document_id": null,
    "investment_document_id": null,
    "address_id": null,
    "phone": null,
    "investor_type": null,
    "suitability_response_document_id": null,
    "is_fully_accredited": false,
    "vi_identifier": null,
    "vi_user_id": null,
    "vi_verification_request_id": null,
    "vi_investor_url": null,
    "vi_verification_status": "unverified"
  },
  "relationships": {
    "deal": {
      "data": null
    },
    "address": {
      "data": null
    }
  }
}
```

FIELDS

Name | Type | Description
---- | ---- | -----------
id | integer | Unique identifier for the object.
type | string | String representing the object's type. Objects of the same type share the same value.
titled | string | String representing what specific investment vehicle owns this investment.
amount | positive integer | A positive integer representing how much this investment will supply.
created_at | timestamp | Time at which the object was created. Stored in ISO8601, and transmitted in UTC.
completed_on | timestamp | Time at which the investment was completed. Stored in ISO8601, and transmitted in UTC.

## Relationships

Name | Relationship
---- | ------------
Processes | An investment can have a variety of concurrent processes which need to be fulfilled on it.
Tasks | An investment can have a variety of tasks, through processes.

## Status

When an investment is underway, there are a variety of processes across
different areas that need to happen before the investment can
successfully be included in part of the deal.

Category | Situation
---- | ------------
Accreditation | The investor must have current/valid accreditation
Subscription | Subscription documents between the two parties must be signed
Suitability | (Potentially) Suitability documents must be signed & approved by the investor's advisor
Escrow | (Potentially) Money must go into escrow
Other | Etc

All these processes need to be able to run concurrently, but in certain
circumstances they might have dependencies upon each other.

<aside class="notice">
Example: Before a sponsor can countersign, the investor's advisor must sign off on the suitability of the investment.
</aside>

Additionally, processes can potentially be different from investment to
investment inside the same deal.

<aside class="notice">
Example: One investment uses Verify Investor to confirm the investor is
accredited. Another might already know the investor is accredited and
not need this process.
</aside>

An investment can have a variety of **processes** required for successful completion.

To track and record where a given process is at, each **process** has an ordered list of **tasks**.

A **notification** is produced when, in order for a **task** to be
completed, a user must take action.

### Process Category
If multiple processes can all address the same underlying need, then
they belong to the same category. Currently, we support 4 different
categories:

Category | Description
---- | ------------
Accreditation | Verifying the investor is accredited.
Subscription | Subscription documents between the two parties must be signed.
Suitability | Suitability documents that must be signed & approved by the investor's advisor
Escrow | Money must go into escrow.


Name | param | Relationship
---- | ----- | ------------
Templates | template | What templates belong to this category.


### Process Template
A real-world sequence of events which take place around an investment.
This stores information about a process that applies to all investments.

**Relationships:**

Name | Relationship
---- | ------------
Category | What underlying category this process template applies to.

### Process
A real-world sequence of events which take place around an investment.
This stores information about a process that's specific to a particular
investment.

### Task
An individual thing that must be done, either by a person, or by the system, in order for the process to advance. (Ex: Investor Signing the subscription documents).

### Notification
An actual notice sent up to a user either informing them of where a process is at, or prompting them to do something to advance a process.

### Process Option
