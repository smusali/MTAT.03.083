## Assignment 1
```
MTAT.03.083_ENG: Assignment #1 - Class modelling | TÜ Moodle

Assignment #1 - Class modelling
Opened: 26.09.2023 00:00:00
Due: 15.10.2023 23:59:00
SM2023 assignment #1
```

- **Task #1 (3 points)**: Please provide a description of the system you will be modelling in this course. Make sure that it matches the designed model as closely as possible and that all details (classes, their attributes, relationships between classes etc.) are specified in both the model and the description. Describe relationships between elements of the system (incl., multiplicity) to provide an unambiguous understanding of the system and the model implying from its description. **NB**: more details can / will be added as the project evolves, and you are expected to provide a description that satisfies the given task, i.e., class model for this assignment. Expected length – ½ - 1 A4 page. The system has to have several types of users (different roles), and the total number of classes should be higher than 5.

- **Task #2 (5 points)**: Provide a class model for the system you described in Task #1. Make sure it is as detailed as necessary (!). Make sure you use at least the following elements: class, attributes, associations, generalization, enumeration, derived data, abstract class, qualifier, role.

- **Task #3 (*1 point*)**: What is the environment, which you choose to design your class diagram? What were the decisive factors to give the preference to this environment? (*+1* point): Does it allow you to generate the code from the designed model? If yes, what are your observations regarding the generated code? Have you identified any weakness in it? Does the code match the designed model? If not, were the expectations-reality differences due to deficiencies in the original model that you were forced to correct?

- **Task #4 (1 point)**: Provide evidence that the work was conducted in a team (e.g., in the form of a link to the VCS; the screenshot of the above etc.).

- **Task #5 (optional)**: Explore and document ChatGPT or other LLM capabilities in modelling class model (in addition to Task#2, but not instead!). Was it possible to achieve the same result that you obtained in Task #2? If not, what were the differences? What are strengths and weaknesses of ChatGPT in addressing this task? Had the use of ChatGPT allowed you to improve either the description (Task#1) or the model (Task#2)? E.g., check if something like this is possible feeding your model?

What to submit? Please submit the homework as a single file – .pdf or a package, if more than one files where created - zip file or .7z file or .tar.gz via [Moodle](https://moodle.ut.ee/mod/assign/view.php?id=1195995)

Please organize and name the files in the package clearly, so that it is clear which file(s) corresponding to the first task and which ones correspond to(MTAT.03.083) the second task.

If you have completed the homework with another (teams of up to four), please write the name of your team-mate in the "Comments" field of the homework submission form. Only one submission per pair of students is needed.

### Reminder on Plagiarism Policy
We don't want to have to say the following, but it's better to say it upfront. Please be reminded that plagiarism in any form is not tolerated. We will be reporting all cases where we have some evidence of plagiarism. You can get an F in the entire course due to a small amount of plagiarism. Whatever you submit, it must be 100% the product of the work of you and your teammate (using AI assistants if you wish). For the same reason, do not share your solution or a partial solution with others (except with your team-mate).

### Use of ChatGPT or Other Large Language Models (LLMs)
Notwithstanding the above note about plagiarism, you can use ChatGPT or similar LLM-based assistants for this homework, provided that you explicitly state in your homework which AI assistant(s) you have used. Warning: If you use them in a trivial manner, you will most likely get an answer that won't meet our requirements and expectations.

## Grable Scenario
Grable, a digital platform, facilitates interactions between two main user entities: restaurants and diners, each required to establish an authorized account for secure and customized access.

Restaurants on Grable possess accounts with distinct attributes: a unique identifier, name, a composite location attribute (address, city, state, postal code), phone number, email, and a dynamic menu. This menu, a collection of items, holds specific attributes for each item: unique identifier, name, a string of aggregated ingredients, dietary specifications, category (such as appetizer, entrée, dessert, etc.), price, and availability status. Restaurants can enable real-time CRUD (Create, Retrieve, Update, and Delete) operations on these menu items, adjusting to current availability or other considerations.

Diner accounts, while also containing a unique identifier, name, phone number, and email, differ by including dietary preferences and a list of payment methods, each a complex type holding details like the payment method type and necessary transaction information. Diners' interaction with Grable involves browsing these dynamic menus and placing orders. An order, a separate entity, includes its unique identifier, a list of item references, a timestamp, table number, and two enumerations for tracking: order status (Pending, In-Progress, Completed, Canceled) and payment status (Unpaid, Paid, Refunded), ensuring diners select only from available items.

Payment processing in Grable is integral, functioning through a secure subsystem that accommodates various payment methods (enumerated as Card, Apple Pay, and Google Pay) and records each transaction with its amount, chosen payment method, and an enumeration for transaction status (Successful, Failed, Pending). After processing, payments are directed to the appropriate restaurant, with a commission subtracted, requiring precise financial handling.

Grable's system architecture emphasizes security through authentication and authorization, real-time data interactions, and user customization, extending to real-time notifications for order and payment updates. Its backend structure is scalable, prepared for an expanding user base and increased transactions, and it maintains system logs and monitoring for performance assessment and irregularity identification.

## System Modeling Analysis of Grable
### Classes
- **User** (Abstract Class):
	- **Attributes**:
		- **uniqueIdentifier**: String
		- **name**: String
		- **phoneNumber**: String
		- **email**: String
	- **Methods**:
		- **createAccount()**: void
		- **authenticate()**: void
- **Restaurant** (subclass of User):
	- **Attributes**:
		- **location**: String (composite of address, city, state, postal code)
		- **menu**: Menu
	- **Methods**:
		- **updateMenu(menuItem: MenuItem, operation: String)**: void (handles CRUD operations)
		- **receivePayment(payment: Payment)**: void
- **Diner** (subclass of User):
	- **Attributes**:
		- **dietaryPreferences**: String
		- **paymentMethods**: List<PaymentMethod> (complex type, not a class)
	- **Methods**:
		- **placeOrder(order: Order)**: void
		- **browseMenu(restaurant: Restaurant)**: List<MenuItem>
- **Menu**:
	- **Attributes**:
		- **items**: List<MenuItem>
	- **Methods**:
		- **addItem(item: MenuItem)**: void
		- **removeItem(item: MenuItem)**: void
		- **updateItem(item: MenuItem)**: void
		- **getItem(id: String)**: MenuItem
		- **listAvailableItems()**: List<MenuItem>
- **MenuItem**:
	- **Attributes**:
		- **uniqueIdentifier**: String
		- **name**: String
		- **ingredients**: String (aggregated details)
		- **dietarySpecifications**: String
		- **category**: Category (enumeration: APPETIZER, ENTREE, DESSERT)
		- **price**: Double
		- **isAvailable**: Boolean
	- **Methods**:
		- **markAvailability(status: Boolean)**: void
- **Order**:
	- **Attributes**:
		- **uniqueIdentifier**: String
		- **items**: List<MenuItem>
		- **timestamp**: DateTime
		- **tableNumber**: String
		- **orderStatus**: OrderStatus (enumeration: PENDING, IN_PROGRESS, COMPLETED, CANCELED)
		- **paymentStatus**: PaymentStatus (enumeration: UNPAID, PAID, REFUNDED)
	- **Methods**:
		- **updateOrderStatus(status: OrderStatus)**: void
		- **updatePaymentStatus(status: PaymentStatus)**: void
- **Payment**:
	- **Attributes**:
		- **amount**: Double
		- **paymentMethod**: PaymentMethod (enumeration: CARD, APPLE_PAY, GOOGLE_PAY)
		- **transactionStatus**: TransactionStatus (enumeration: SUCCESSFUL, FAILED, PENDING)
	- **Methods**:
		- **processPayment()**: void
		- **refundPayment()**: void

### Relationships
- Restaurant has a one-to-one relationship with Menu. Each restaurant has one menu, and each menu is associated with one restaurant.
- Menu has a one-to-many relationship with MenuItem. A menu comprises multiple menu items.
- Diner has a one-to-many relationship with Order. A diner can place multiple orders.
- Order has a many-to-many relationship with MenuItem. An order can contain multiple menu items, and a menu item can be part of multiple orders.
- Order has a one-to-one relationship with Payment. Each order initiates one payment process.
- Restaurant and Diner are subclasses of User, indicating a generalization relationship where both restaurant and diner accounts share common attributes from the User class but also have unique features.

### Enumerations
- **OrderStatus**: PENDING, IN_PROGRESS, COMPLETED, CANCELED
- **PaymentStatus**: UNPAID, PAID, REFUNDED
- **TransactionStatus**: SUCCESSFUL, FAILED, PENDING
- **PaymentMethod**: CARD, APPLE_PAY, GOOGLE_PAY
