# Rolling back + Atomic Operations in ERP

## Problem statement

There are some sets of operations in ERP we need to consider ‘Atomic’, or as one action.

For example, these crucial lines must be executed together, or not at all.

```python
payment_gateway = StripePaymentGateway()
payment_intent_id = payment_gateway.execute_payment_request(session, self, payment_method)

# We must create a payment entry and sales invoice if the payment went through.
# An error here is a disaster. The payment has already happened yet we cannot save the info in our system.
self.create_payment_entry()
sales_invoice = SalesInvoice.create_from_sales_order(self.reference_name)
```

## Solution

The frappe framework actually already handles this for us!

[https://frappeframework.com/docs/user/en/api/database#database-transaction-model](https://frappeframework.com/docs/user/en/api/database#database-transaction-model)

<aside>
💡 Frappe API Requests

- While performing `POST` or `PUT`, if any writes were made to the database, they are committed at end of the successful request.
- AJAX calls made using `frappe.call` are `POST` by default unless changed.
- `GET` requests do not cause an implicit commit.
- Any **uncaught** exception during handling of request will rollback the transaction.
</aside>

We can be explicit about our needs as well

```python
# Frappe API calls inherently begin with a frappe.db.begin()
# db.begin() is just doing sql START TRANSACTION. MariaDB implicitly commits the previous transaction on starting a new one.

frappe.db.begin()

doc = new_doc("any_doc")
doc.insert()

frappe.db.commit()
# Frappe db commit closes out the current transaction and opens a new one
# This new transaction will be closed again as the API call completes with 200
```

Remember that frappe will rollback any database changes if an error (frappe.throw) is thrown. 

```python
doc = new_doc("any_doc")
doc.insert()
# doc will not be inserted, as an error is thrown before API completion

# frappe.db.commit() # Uncomment this line to insert the document, regardless of error

frappe.throw("Error!")

```

## Specifying API Methods (replacing @whitelist)

I think we have been getting lucky and/or not understanding why some objects are not saved, so we end up putting frappe.db.commit() in random locations to solve our issues.

```python
@Whitelist
def get_data():
		data = data()
		
		record = frappe.new_doc("Record")
		record.insert()
		
		# Not working? Try frappe.db.commit() I guess
		
		return data
```

<aside>
💡 If this endpoint is called from the client as a ‘Get’, record is never inserted into the database.
If the endpoint is called as a ‘Post’, record will be saved.

</aside>

### Resolution

When writing backend endpoints we should specify what method we expect to be used when calling the function. 

[@Get and @Post](https://bitbucket.org/biiibo-dev/biiibo_app/pull-requests/493) should be used to indicate correct usage of an API

```python
import biiibo_app.utils.api as API

@API.Post
def get_data():
		data = data()
		
		record = frappe.new_doc("Record")
		record.insert()
		
		return data
```