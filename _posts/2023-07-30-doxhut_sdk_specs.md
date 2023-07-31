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

# DoxHut SDK Documentation

## Introduction

Currently, **pepsico-ru** drivers utilize the **iSales** mobile application to manage their routes and handle delivery-related tasks. To streamline their operations and enhance efficiency, we aim to integrate their existing ERP route import solution with **DoxHut**. To achieve this, we will create a robust API structure that facilitates seamless integration between their **ERP** system and **DoxHut**. <br>

Additionally, we will develop a **DoxHut SDK**, which will enable their **iSales** app to interact with specific endpoints on the **DoxHut API**.

### **DoxHut Driver Flow**

![intro](/assets/images/images-sdk-driver-flow.png)

## DoxHut SDK - Library - Methods

### Start Route

**Goal**

- Start a route from a host application on the **DoxHut Server** via the **DoxHut Engine**.<br>

**Background and Strategic Fits**

- On **pepsico-ru**, routes are currently initiated from the origin using the **iSales** app.
- Currently, routes are imported from **ERP** into **iSales**.<br>

**Assumptions**

- Routes will be imported from **ERP** to **DoxHut**, containing all necessary information for successful loading on both the host app and **DoxHut Engine**.
- System administrators will configure and maintain driver configurations, permissions, and route action restrictions on **DoxHut Live**.

#### **Requirements**

- Make it possible for **Pepsico RU** drivers to start routes from a host app to the **DoxHut Server** via the **DoxHut Engine**.

#### **User Story**

As an **iSales** user from **Pepsico RU**'s operation, I need to be able to start routes.

#### **DoxHut Engine Method**

- Starts the route loaded by the user and changes its status to **"in progress"**.<br>

**Throws:**
- **TenantNotDefinedException** when no tenant has been informed.
- **NoRouteLoadedExceptio** when no route has been loaded.
- **RouteAlreadyStartedException** when the route has already been started.
- **NetworkErrorException** when it was not possible to establish communication with the server. 
<br>

> **Note**: Communication errors, lack of connectivity, or when the server is down may cause **NetworkErrorException**.

##### **Flow**

###### Success Scenario 1 - Successfully start route

- **DoxHutEngine.startRoute** is called successfully.<br>

**Requirements:**
- Communication with the server.
- The driver must have previously loaded the route.
- The route could not have been previously started.<br>

###### Failure Scenario 1 - Network error 

- **DoxHutEngine.startRoute** is called, then **NetworkErrorException* is thrown.<br>

**Requirements:**
- Communication with the server.<br>

###### Failure Scenario 2 - No route loaded

- **DoxHutEngine.startRoute** is called, then **NoRouteLoadedException** is thrown.<br>

**Requirements:**
- Communication with the server.
- The driver must have not previously loaded the route.<br>

###### Failure Scenario 3 - Route already started

- **DoxHutEngine.startRoute** is called, then **RouteAlreadyStartedException** is thrown.<br>

**Requirements:**
- Communication with the server.
- The driver must have previously loaded the route.
- The route could not have bee previously started.<br>

##### **Acceptance Criteria**

- Verify whether the route status changes to **STARTED** after executing the start route action.
- Verify whether any other route changes its status to **STARTED** after execunting this action.
- Verify whether this method uses the **Request Queue** correclty.<br>

### Complete Route

**Goal**

- Complete routes from a host application on the **DoxHut Server** via the **DoxHut Engine**.<br>

**Background and Strategic Fits**

- On **pepsico-ru** operation, routes are currently departed from the origin using the **iSales** app.
- Currently, routes are imported from **ERP** into **iSales**.<br>

**Assumptions**

- Routes will be imported from **ERP** to **DoxHut**, containing all necessary information for successful loading on both the host app and **DoxHut Engine**.
- System administrators will configure and maintain driver configurations, permissions, and route action restrictions on **DoxHut Live**.

#### **Requirements**

- Make it possible for **pepsico-ru** drivers to complete routes from a host app to the **DoxHut Server** via the **DoxHut Engine**.<br>

#### **User Story**

- As an **iSales** user from **pepsico-ru**'s operation, I need to be able to inform the **DoxHut Engine** when I complete a route.<br>

#### **DoxHut Engine Method**

- Action input by the driver or system administrator to indicate the route has been completed.<br> 

> **Note**: This is the last route action possible and can only be performed once the driver arrived at the destination and all stops are in a status different than **"pending"**.<br>

**Throws:**
- **TenantNotDefinedException** when no tenant has been informed.
- **StillNotArrivedAtDestination** when the action **"Arrive at Destination"** has not yet been performed.
- **NoRouteLoadedException** when no route has been loaded.
- **NetworkErrorException** when it was not possible to establish communication with the server.
<br>  

> **Note**: Communication errors, lack of connectivity, or when the server is down may cause **NetworkErrorException**.<br>

#### **Flow**

##### **Success Scenario 1 - It is called DoxHutEngine.completeRoute with success**

**Requirements:**
- The driver must have previously executed the **Arrive at Destination** method.
- Communication with server.
- The driver must have previously loaded the route.<br>

##### **Failure Scenario 1 - Network error**
- **DoxHutEngine.completeRoute** is called, then **NetworkErrorException** is thrown.<br>

**Requirements:**
- It must not be able to communicate with the server.<br>

##### **Failure Scenario 2 - No route loaded**
- **DoxHutEngine.completeRoute** is called, then **NoRouteLoadedException** is thrown.<br>

**Requirements:**
- Communication with server.
- The driver must have not previously loaded the route.<br>

##### **Failure Scenario 3 - Still not arrived at the destination**
- **DoxHutEngine.completeRoute** is called, then **tillNotArrivedAtDestination** is thrown.<br>

**Requirements:**
- The driver must have not previously executed the **Arrive at Destination** method.
- Communication with server.
- The driver must have previously loaded the route.<br>

#### **Acceptance Criteria**

- Verify whether the route status changes to **COMPLETED** after executing the complete route action.
- Verify whether any other route changes its status to **COMPLETED** after executing this method.
- Ensure it is not possible to complete the route without having previously executed the **Arrive at Destination** method.<br>


[Back to Home Page](/)