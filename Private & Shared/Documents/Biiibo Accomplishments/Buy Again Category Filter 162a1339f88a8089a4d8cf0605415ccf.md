# Buy Again Category Filter

# Spec: Buy Again Category Filter

Tags: ERP
Date: August 29, 2024
Lead SDE: Justin Lycklama
Status: In progress

## Overview

Our buy again page paginates items since they were most recently bought.

We would like to add some detail to this page to make it more useful for users.

Our current buy again page looks identical to all items page.

The search bar at the top **does not** search buy again products, but searches all products.

![](https://www.notion.soTech%20Spec%20Buy%20Again%20Category%20Filter%2001f18955dd724d41a93097f3a3796e17/simulator_screenshot_361016BD-E9A6-4B39-8940-CE12A23845EE.png)

simulator_screenshot_361016BD-E9A6-4B39-8940-CE12A23845EE.png

# Potential Additions

### 1. Categorize Items

We could add the option to view the buy-again items by category.

The user would be able to select from a list of categories they have purchased from, and the paginated list would be filtered by category

![](https://www.notion.soTech%20Spec%20Buy%20Again%20Category%20Filter%2001f18955dd724d41a93097f3a3796e17/Simulator_Screenshot_-_iPhone_15_-_2024-08-20_at_15.00.21.png)

Simulator Screenshot - iPhone 15 - 2024-08-20 at 15.00.21.png

## 2. Search by Name

We could change the top bar to search the buy again products by name, instead of using the same Algolia based search the rest of the application uses

## 3. Display by Date and/or by Order

Looking at amazon’s buy again page, they split their rows into sections, with the section headers being:

- Date the order was purchased
- Order number

![](https://www.notion.soTech%20Spec%20Buy%20Again%20Category%20Filter%2001f18955dd724d41a93097f3a3796e17/Screenshot_2024-08-20_at_3.07.19_PM.png)

Screenshot 2024-08-20 at 3.07.19 PM.png

# Deep Dive

Existing data structure

### Order Again

Only one document per customer, with two fields.

| Type | Doctype | Description |
| --- | --- | --- |
| **Link** | Customer | The customer this order again info belongs to |
| **Table** | Order Again Item | a list of order again items |

### Order Again Item

Simply a reference to the purchased item

| Type | Doctype | Description |
| --- | --- | --- |
| **Link** | Item | The item document the customer purchased |

---

# Proposed Solutions

## 1. Categorize Items

To get the total available buy again categories and the products for those categories, we will have to update our data structure. We essentially need a map from a category to a list of items

```python
"categories": {
      "Type1": {"item_code1", "item_code3", ...},
      "Type2": {"item_code2", "item_code4", ...},
  }
```

### Option 1

We can create yet another doctype

### Order Again Category Map

| Type | Doctype | Description |
| --- | --- | --- |
| **Link** | ItemGroup | The Category |
| **Table** | Order Again Item | a list of order again items |

The Order Again Items would already exist in the database, we would just be creating another mapping to it.

### Order Again

| Type | Doctype | Description |
| --- | --- | --- |
| **Link** | Customer | The customer this order again info belongs to |
| **Table** | Order Again Item | a list of order again items |
| **Table** | Order Again Category Map | A list of ‘maps’ (A category and list of associated items) |

### ~~Option 2~~

~~We could also just store a raw json dictionary in the Order Again doctype~~

[~~https://frappeframework.com/docs/user/en/basics/doctypes/fieldtypes#code~~](https://frappeframework.com/docs/user/en/basics/doctypes/fieldtypes#code)

## 2. Search by Name

Add the item name onto the Order Again Item doctype

### Order Again Item

| Type | Doctype | Description |
| --- | --- | --- |
| **Link** | Item | The item document the customer purchased |
| **String** | - | Item Name |

Add a filter option to get_order_again_items, with included search term

```python
def get_order_again_items(session: Session,
start: int = 0,
limit: int = 5,
search_term: str = nil)
-> [str]:
...
order_again_doc = frappe.get_doc("Order Again", existing_order_again_name)
start = int(start) if isinstance(start, str) else start
limit = int(limit) if isinstance(limit, str) else limit
filtered_items = order_again_doc.items.filter(search_term)
paginated_items = filtered_items[start:start + limit]
return [item.item_code for item in paginated_items]
```

---

💡 This is basically a different project. Maybe make these changes instead?

# 3. Display by date and/or Order

Once again, take a look at Amazon’s return page.

1. Order Placed Date
2. Order number (View order details, status)
3. All Items placed from said order
4. Buy again on all items in list

![](https://www.notion.soTech%20Spec%20Buy%20Again%20Category%20Filter%2001f18955dd724d41a93097f3a3796e17/Screenshot_2024-08-20_at_3.07.19_PM.png)

Screenshot 2024-08-20 at 3.07.19 PM.png

### Reimagined ‘My Orders’ Page

Our current Orders page lists the order number, shows **one** item from the list of items we have ordered, and displays the order status.

If we imagine the table as being sectioned instead:

- The header for each section could have details on the order date and payment status
- Tapping the header would bring you to the standard Order Details Page
- Under the header would be a list of products purchased in that order, with the ability to re-add to cart.

![](https://www.notion.soTech%20Spec%20Buy%20Again%20Category%20Filter%2001f18955dd724d41a93097f3a3796e17/simulator_screenshot_7E3FC0B0-1BCC-4233-BA47-CA77BBB37AD6.png)

simulator_screenshot_7E3FC0B0-1BCC-4233-BA47-CA77BBB37AD6.png

![](https://www.notion.soTech%20Spec%20Buy%20Again%20Category%20Filter%2001f18955dd724d41a93097f3a3796e17/stickyHeader.gif)

stickyHeader.gif

If we moved to this model, we could delete the Order Again Item Doctype

### ~~Order Again Item~~

| Type | Doctype | Description |
| --- | --- | --- |
| **Link** | Item | The item document the customer purchased |
| **String** | - | Item Name |

This doctype is inferior to the already existing **Sales Order Item,** which is already populated with many fields

Under this layout, our **Order Again** and **Order Again Category Map** will now point to Sales Order Item instead of Order Again Item

### Order Again

| Type | Doctype | Description |
| --- | --- | --- |
| **Link** | Customer | The customer this order again info belongs to |
| **Table** | Sales Order Item | a list of Sales Items |
| **Table** | Order Again Category Map | A list of ‘maps’ (A category and list of associated items) |

### Order Again Category Map

| Type | Doctype | Description |
| --- | --- | --- |
| **Link** | ItemGroup | The Category |
| **Table** | Sales Order Item | a list of order again items |

## Endpoints

| Endpoint | Input | Output | Description |
| --- | --- | --- | --- |
| /url |  |  |  |
|  |  |  |  |

## Timelines

This will get moved over to the project doc that your PM owns. Feel free to work on this with them.

| Milestone | Allocated Time in days | Start Date | End Date | Owner | Description |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |
|  |  |  |  |  |  |

when coming up with dates, make sure to account for your and your teams on-call schedule, vacation, holidays, etc.

## Appendix

Include related/referenced documents, links.

Example tech specs :

- [https://www.notion.so/biiibo/Tech-Spec-Multiple-Carts-751a1956522444e69a60e1a156551fdc](https://www.notion.so/751a1956522444e69a60e1a156551fdc?pvs=21)