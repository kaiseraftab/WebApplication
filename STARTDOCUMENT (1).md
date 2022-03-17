# Startdocument for Pizza Delivery Service

Startdocument of **Oleksandr Sikora**. Student number **4799925**.

## Problem Description

We need to create a program that can track delivery expenses. This application stores a list of individual deliveries, keeping track of who was the deliverer, whether they were using a bike or a scooter, length of the route and the date of the delivery. Costs of delivery per kilometre are: 0,12 euros with a scooter; 0,02 euros with a bike. Each deliverer gets a daily loan. The loan is used to pay for the delivery expenses done by the deliverer. The deliverer can't do a delivery if its cost is bigger than the remainder of the daily loan. This application can provide an overview of all expenses grouped into months, and of the most earning pizza deliverer. The most earning pizza deliverer is the one that has done the most deliveries.

- Create an environment that is able to store a list of deliveries with the necessary data
- Create a method that adds deliveries and checks the deliverer's loan to see if it's possible beforehand
- Create a method that lists all the expenses per month
- Create a method that displays the deliverer with the most deliveries



### Input and Output

In this section the in- and output of the application will be described.

#### Input

|          Case           |    Type     | Conditions                      |
| :---------------------: | :---------: | :------------------------------ |
|     Deliverer name      |  `String`   | not empty                       |
| Deliverer date of birth | `LocalDate` | not empty, format: "dd/MM/yyyy" |
|      Delivery date      | `LocalDate` | not empty, format: "dd/MM/yyyy" |
|         Vehicle         |  `Vehicle`  | Scooter or Bike                 |
|      Route length       |  `integer`  | not empty                       |

#### Output

|                Case                |                             Type                             |
| :--------------------------------: | :----------------------------------------------------------: |
|     Monthly expenses overview      | `String`<br />Format: "[Year] [Month]: [Sum of expenses of that month] euros"<br />Example: "2021 March: 25,12 euros" |
| Overview of most earning deliverer | `String`<br />Format: "[Name of deliverer] - [number of deliveries] deliveries"<br />Example: "John Doe - 12 deliveries" |

#### Calculations

|      Case      |                Type                |
| :------------: | :--------------------------------: |
| Deliverer loan |    Age of deliverer * 1.5 - 2.5    |
| Delivery cost  | Route length * vehicle cost per km |

## Class Diagram 

![img](image-20211005113916707.png)

## Test plan 

### Test Data

In the following table you'll find all the data that is needed for testing.

<h4>Deliverer</h4>

| ID          | Input                                         | Code                                        |
| ----------- | --------------------------------------------- | ------------------------------------------- |
| `johnDoe`   | name: John Doe<br />dateOfBirth: 29/03/1991   | `new Deliverer("John Doe", "29/03/1991")`   |
| `mattPratt` | name: Matt Pratt<br />dateOfBirth: 29/03/2001 | `new Deliverer("Matt Pratt", "29/03/2001")` |

<h4>Vehicle</h4>

| ID         | Input | Code            |
| ---------- | ----- | --------------- |
| `scooter1` |       | `new Scooter()` |
| `bike1`    |       | `new Bike()`    |
<h4>Delivery</h4>

| ID          | Input                                                        | Code                                        |
| ----------- | ------------------------------------------------------------ | ------------------------------------------- |
| `delivery1` | dateOfDelivery: 05/10/2021<br />vehicle: scooter1<br />routeLength: 50 | `new Delivery("05/10/2021", scooter1, 50)` |
| `delivery2` | dateOfDelivery: 01/09/2020<br />vehicle: bike1<br />routeLength: 80 | `new Delivery("01/09/2020", bike1, 80)`     |
| `delivery3` | dateOfDelivery: 02/09/2020<br />vehicle: bike1<br />100      | `new Delivery("02/09/2020", bike1, 100)`    |
<h4>Store</h4>

| ID      | Input | Code          |
| ------- | ----- | ------------- |
| `store` |       | `new Store()` |
<h4>Attach deliveries and deliverers to store</h4>

| ID           | Input                                         | Code                                |
| ------------ | --------------------------------------------- | ----------------------------------- |
| `deliveries` | deliverer: johnDoe<br />delivery: delivery1   | `addDelivery(johnDoe, delivery1)`   |
| `deliveries` | deliverer: mattPratt<br />delivery: delivery2 | `addDelivery(mattPratt, delivery2)` |
| `deliveries` | deliverer: mattPratt<br />delivery: delivery3 | `addDelivery(mattPratt, delivery3)` |

<h3>Test Cases</h3>

In this section the testcases will be described. Every test case should be executed with the test data as starting point.

<h4>#1 Get loan amount</h4>

| Step | Input | Action            | Expected output           |
| ---- | ----- | ----------------- | ------------------------- |
| 1    |       | johnDoe.getLoan() | 30 • 1,5 - 2,5 = **42,5** |

<h4>#2 Get cost of delivery</h4>

| Step | Input | Action              | Expected output   |
| ---- | ----- | ------------------- | ----------------- |
| 1    |       | delivery1.getCost() | 50 • 0.12 = **6** |

<h4>#3 Get monthly overview</h4>

| Step | Input | Action                          | Expected output                            |
| ---- | ----- | ------------------------------- | ------------------------------------------ |
| 1    |       | deliveries.getMonthlyOverview() | "2020 September: 3,6<br />2021 October: 6" |

<h4>#4 Get overview of most earning deliverer</h4>

| Step | Input | Action                              | Expected output             |
| ---- | ----- | ----------------------------------- | --------------------------- |
| 1    |       | deliveries.getMostEarningOverview() | "Matt Pratt - 2 deliveries" |

<h4>#5 Get deliverer age</h4>

| Step | Input | Action           | Expected output |
| ---- | ----- | ---------------- | --------------- |
| 1    |       | johnDoe.getAge() | 30              |

<h4>#6 Attempt to add a delivery that is beyond the deliverers loan</h4>

| Step | Input                           | Action                                       | Expected output                         |
| ---- | ------------------------------- | -------------------------------------------- | --------------------------------------- |
| 1    | 02/09/2020<br />true<br />10000 | Delivery delivery4 = new Delivery()          | Delivery created                        |
| 2    | mattPratt<br />delivery4        | deliveries.addDelivery(mattPratt, delivery4) | "The cost of this delivery is too high" |