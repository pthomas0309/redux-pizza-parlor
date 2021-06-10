- [ ] Pizza Cart!

- [ ] Reducers Needed
    - [ ] Pizzas in cart (attatched to '/api/order' on server)
        - [ ] named:     pizzaCart
        - [ ] Select (dispatch) a pizza 
        - [ ] Remove a pizza from cart (state)

        // TO DO: Decide on data model for cart state re. total
        - [ ] start at state = {totalPrice: 0, pizzasInCart: []}
        - [ ] actions:
            - [ ] 'ADD_PIZZA'
                    - [ ] payload: the pizza object that was sent 
                    - [ ] handle logic for total cost when returning
                        STRETCH: quantity: number chosen    
            - [ ] 'REMOVE_PIZZA'
                - [ ] Will need filter
                - [ ] compare id of item to remove to state of pizzaCart
            - [ ] 'ORDER_SUBMITTED'
                - [ ] will need to reset state after POST route is done

    - [ ] customer information 
        - [ ] named:  customerDetails
        - [ ] state = {} 
        - [ ] actions: 
            - [ ] 'SUBMIT_CUSTOMER'
                - [ ] action.payload is a customer object to become state
            - [ ] 'ORDER_SUBMITTED'
                - [ ] reset state    
        


- [ ] useSelector to get all pizzas when looking to POST order
    - [ ] get from pizza cart


- [ ] Front-end stuff
 !!   ROUTE NAME: '/menu'    !!
    - [ ] GET from database: full pizza menu (attatched to '/api/pizza' on server)
        - [ ] Display on DOM
            - [ ] each menu item as individual div with:
                - [ ] pizza pic
                - [ ] pizza name && price && description
                - [ ] ADD/REMOVE button (rendered conditionally based on if the pizza has been added to the cart)
            

    - [ ] Ability to choose a pizza from menu and a quantity?
    - [ ] Dispatch to pizzaCart reducer (type: 'ADD_PIZZA')
        - [ ] payload should be entire pizza object as well as quantity
        - [ ] payload: {
                pizza(info from DB): pizzaFromMenu <-- this is an object
                quanity: number
              }
    
    - [ ] Ability to remove pizza from cart
        - [ ] payload: the pizza object that was chosen
    - [ ] next button
        - [ ] navigate to '/customerinfo' route


  !!    ROUTE NAME: '/customerinfo'      !!
    - [ ] local states to hold form data
    - [ ] Inputs
        - [ ] customer_name
        - [ ] street_address
        - [ ] city
        - [ ] zip
        - [ ] type
            - [ ] radio input
            - [ ] pickup or delivery
     
     - [ ] Display total
        - [ ] useSelector pizzaCart
    - [ ] button for form
        - [ ] 'SUBMIT_CUSTOMER' action
        - [ ] payload: customer object that was pulled from input values, include     total price
    - [ ] sends client to '/checkout' route 

- [ ] checkout screen
    - [ ] customer info
        - [ ] from customerDetails reducer
    - [ ] table with pizzas ordered
        - [ ] from pizzaCart reducer
    - [ ] Total
    - [ ] checkout button
        - [ ] POST request with all data brought in
        - [ ] 'ORDER_SUBMITTED' action to all reducers
        - [ ] confirmation dialog
        - [ ] navigate to '/menu' route







Data Model

Database Name:
pizza_parlor


"pizza" (
	"id" SERIAL PRIMARY KEY,
	"name" VARCHAR(100) NOT NULL,
	"description" VARCHAR(1000) NOT NULL,
	"price" NUMERIC (20, 2) NOT NULL,
	"image_path" VARCHAR(1000) NOT NULL
)


"orders" (
	"id" SERIAL PRIMARY KEY,
	"customer_name" VARCHAR (1000) NOT NULL,
	"street_address" VARCHAR(1000) NOT NULL,
	"city" VARCHAR(1000) NOT NULL,
	"zip" VARCHAR(20) NOT NULL,
	"type" VARCHAR(100) NOT NULL, either pickup or delivery
	"total" NUMERIC (20, 2) NOT NULL, 


	"time" TIMESTAMP DEFAULT NOW() NOT NULL
);


**Example JSON Post Data:**

```JSON
{
  "customer_name": "Donatello",
  "street_address": "20 W 34th St",
  "city": "New York",
  "zip": "10001",
  "total": "27.98",
  "type": "Pickup",
  "pizzas": [{
    "id": "1",
    "quantity": "1"
  },{
    "id": "2",
    "quantity": "1"
  }]
}

