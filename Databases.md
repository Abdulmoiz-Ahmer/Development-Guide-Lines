# Development-Guide-Lines

**DataBases**

Whether MongoDB, MySQL, or another database format, all databases must use the following conventions:

Table or collection names must be the pluralized version of the asset they contain and must be snake cased. For example, a table containing search queries might be `search_queries` whereas a collection containing real estate agent user data might be agents.

Table column and document field names must be snake cased and should describe the data they contain. Abbreviations are to be avoided unless they are common enough for a layperson to recognize.

Good: `first_name`, `street_address`, `phone_number`.

Bad: `fname`, `addr`, `PhoneNumber`

Column and field names must not contain the the name of the collection or table unless absolutely necessary for clarity. Consider the aforementioned `agents` collection:

Good: `first_name`, `last_name`, `brokerage_id`

Bad: `agent_phone_number`, `agent_first_name`

In general, related fields should be grouped together. When in doubt, arrange fields in alphabetical order.

**Embedded Documents**

Document-oriented database formats such as MongoDB allow for the embedding of documents inside of other documents. Embedded documents should only be used on data that is connected to the parent document and only the parent document and never needs to be accessed without the parent document.

For example, multiple Billing Addresses for a User could be added as embedded documents.

```
{
  "_id": ObjectId("507f1f77bcf86cd799439011"),
  "name": {"first": "Lauren", "last": "Ipsum"},
  "billing_addresses": [
    {
      "_id": ObjectId("507f191e810c19729de860ea"),
      "title": "Home",
      "address": {
        "street": "1407 Graymalkin Lane",
        "city": "Salem Center",
        "state": "New York",
        "zip": "10590"
      }
    },
    {
      "_id": ObjectId("416e2e88cda97de800540122"),
      "title": "Work",
      "address": {
        "street": "177A Bleecker Street",
        "city": "New York",
        "state": "New York",
        "zip": "12834"
      }
    }
  ]
}
```
Whereas embedding agent data on a brokerage would not be allowed. In general, if a document must be queried independently of its parent document it should not be embedded.
