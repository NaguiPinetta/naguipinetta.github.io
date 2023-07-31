---
title: DoxHut SDK Specs
layout: post
post-image: "https://i.ibb.co/cCFJXRF/sdk.png"
description: Putting out fires with docs since 2017
tags:
- Business Requirements
- Technical Writing
- Technical Specification
- SDK Docs
- English

---

## Use Case

🔥 ...

🍍 ...

🚀 ...

<span style="color:darkblue">

# DoxHut SDK Documentation

</span>

<span style="color:black">

## Introduction

</span>

Currently, **pepsico-ru** drivers utilize the **iSales** mobile application to manage their routes and handle delivery-related tasks. To streamline their operations and enhance efficiency, we aim to integrate their existing ERP route import solution with **DoxHut**.

To achieve this, we will create a robust API structure that facilitates seamless integration between their **ERP** system and **DoxHut**.

Additionally, we will develop a **DoxHut SDK**, which will enable their **iSales** app to interact with specific endpoints on the **DoxHut API**.

<span style="color:darkgreen">

### **DoxHut Driver Flow**

</span>

![intro](/assets/images/images-sdk-driver-flow.png)

<span style="color:black">

## DoxHut SDK - Library - Methods

</span>

<span style="color:darkred">

### Start Route

</span>

**Goal**

- Start a route from a host application on the **DoxHut Server** via the **DoxHut Engine**.

**Background and Strategic Fits**

- On **pepsico-ru**, routes are currently initiated from the origin using the **iSales** app.
- Currently, routes are imported from **ERP** into **iSales**.

**Assumptions**

- Routes will be imported from **ERP** to **DoxHut**, containing all necessary information for successful loading on both the host app and **DoxHut Engine**.
- System administrators will configure and maintain driver configurations, permissions, and route action restrictions on **DoxHut Live**.

<span style="color:darkred">

#### **Requirements**

</span>

- Make it possible for **Pepsico RU** drivers to start routes from a host app to the **DoxHut Server** via the **DoxHut Engine**.

<span style="color:darkred">

#### **User Story**

</span>

As an **iSales** user from **Pepsico RU**'s operation, I need to be able to start routes.

<span style="color:darkred">

#### **DoxHut Engine Method**

</span>

- Starts the route loaded by the user and changes its status to **"in progress"**.

**Throws:**
- **TenantNotDefinedException** when no tenant has been informed.
- **NoRouteLoadedExceptio** when no route has been loaded.
- **RouteAlreadyStartedException** when the route has already been started.
- **NetworkErrorException** when it was not possible to establish communication with the server. 

> **Note**: Communication errors, lack of connectivity, or when the server is down may cause **NetworkErrorException**.

<span style="color:darkmagenta">

##### **Flow**

</span>

<span style="color:darkmagenta">

###### Success Scenario 1 - Successfully start route

</span>

- **DoxHutEngine.startRoute** is called successfully.

**Requirements:**
- Communication with the server.
- The driver must have previously loaded the route.
- The route could not have been previously started.

<span style="color:darkmagenta">

###### Failure Scenario 1 - Network error 

</span>

- **DoxHutEngine.startRoute** is called, then **NetworkErrorException** is thrown.

**Requirements:**
- Communication with the server.

<span style="color:darkmagenta">

###### Failure Scenario 2 - No route loaded

</span>

- **DoxHutEngine.startRoute** is called, then **NoRouteLoadedException** is thrown.

**Requirements:**
- Communication with the server.
- The driver must have not previously loaded the route.

<span style="color:darkmagenta">

###### Failure Scenario 3 - Route already started

</span>

- **DoxHutEngine.startRoute** is called, then **RouteAlreadyStartedException** is thrown.

**Requirements:**
- Communication with the server.
- The driver must have previously loaded the route.
- The route could not have bee previously started.

<span style="color:darkmagenta">

##### **Acceptance Criteria**

</span>

- Verify whether the route status changes to **STARTED** after executing the start route action.
- Verify whether any other route changes its status to **STARTED** after executing this action.
- Verify whether this method uses the **Request Queue** correclty.

<span style="color:darkred">

### Complete Route

</span>

**Goal**

- Complete routes from a host application on the **DoxHut Server** via the **DoxHut Engine**.

**Background and Strategic Fits**

- On **pepsico-ru** operation, routes are currently departed from the origin using the **iSales** app.
- Currently, routes are imported from **ERP** into **iSales**.

<span style="color:darkred">

**Assumptions**

</span>

- Routes will be imported from **ERP** to **DoxHut**, containing all necessary information for successful loading on both the host app and **DoxHut Engine**.
- System administrators will configure and maintain driver configurations, permissions, and route action restrictions on **DoxHut Live**.

<span style="color:darkred">

#### **Requirements**

</span>

- Make it possible for **pepsico-ru** drivers to complete routes from a host app to the **DoxHut Server** via the **DoxHut Engine**.

<span style="color:darkred">

#### **User Story**

</span>

- As an **iSales** user from **pepsico-ru**'s operation, I need to be able to inform the **DoxHut Engine** when I complete a route.

<span style="color:darkred">

#### **DoxHut Engine Method**

</span>

- Action input by the driver or system administrator to indicate the route has been completed.

> **Note**: This is the last route action possible and can only be performed once the driver arrived at the destination and all stops are in a status different than **"pending"**.

**Throws:**
- **TenantNotDefinedException** when no tenant has been informed.
- **StillNotArrivedAtDestination** when the action **"Arrive at Destination"** has not yet been performed.
- **NoRouteLoadedException** when no route has been loaded.
- **NetworkErrorException** when it was not possible to establish communication with the server.
  
> **Note**: Communication errors, lack of connectivity, or when the server is down may cause **NetworkErrorException**.

<span style="color:darkmagenta">

#### **Flow**

</span>

<span style="color:darkmagenta">

##### **Success Scenario 1 - It is called DoxHutEngine.completeRoute with success**

</span>

**Requirements:**
- The driver must have previously executed the **Arrive at Destination** method.
- Communication with server.
- The driver must have previously loaded the route.

<span style="color:darkmagenta">

##### **Failure Scenario 1 - Network error**

</span>

- **DoxHutEngine.completeRoute** is called, then **NetworkErrorException** is thrown.

**Requirements:**
- It must not be able to communicate with the server.

<span style="color:darkmagenta">

##### **Failure Scenario 2 - No route loaded**

</span>

- **DoxHutEngine.completeRoute** is called, then **NoRouteLoadedException** is thrown.

**Requirements:**
- Communication with server.
- The driver must have not previously loaded the route.

<span style="color:darkmagenta">

##### **Failure Scenario 3 - Still not arrived at the destination**

</span>

- **DoxHutEngine.completeRoute** is called, then **tillNotArrivedAtDestination** is thrown.

**Requirements:**
- The driver must have not previously executed the **Arrive at Destination** method.
- Communication with server.
- The driver must have previously loaded the route.

<span style="color:darkmagenta">

#### **Acceptance Criteria**

</span>

- Verify whether the route status changes to **COMPLETED** after executing the complete route action.
- Verify whether any other route changes its status to **COMPLETED** after executing this method.
- Ensure it is not possible to complete the route without having previously executed the **Arrive at Destination** method.

[Back to Home Page](/)




[Back to Home Page](/)