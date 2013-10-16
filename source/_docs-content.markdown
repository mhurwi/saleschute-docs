Orders
======

Using Saleschute, you can sell any product from any site.  This section of the API documentation explains:

- how the customer actually purchases a product from your site,
- which API calls and parameters the client sends to the server
- how the server responds


Saleschute uses a small set of Angular.js directives to place an order.

Placing an order on your site follows this sequence:

- Customer sees product on your site and clicks a Saleschute 'add item to cart' button:
  * directive: add_line_item
  * params: variant_id

- Customer views the contents of his cart and makes some changes:
  * directive: update_quantity
  * params: line_item_id, quantity

  * directive: remove_line_item
  * params: line_item_id, remove_line_item (true)

  * directive: update_variant
  * params: line_item_id, variant_id

- Customer proceeds to enter their billing and shipping info
  * directive: create_or_update_customer
  * params: customer[:email], customer[:name], customer[:card_uri], customer[:last4], customer[:address]
    * *note*: customers address should include: street1, city, state, zip

- Customer reviews their info and clicks 'place order'
  * directive: place_order
  * params: place_order ("yes") *should be 'true'*


The first time a customer clicks 'add item to cart', Saleschute will create a new order and set the encrypted order ID on the client, named 'encrypted_client_id'

In every other call, the encrypted_client_id is passed as a param.

In every call, including the initial 'add item to cart' call, the response is the most recent Order object.