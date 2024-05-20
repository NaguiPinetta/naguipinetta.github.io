---
title: Tech Specs / User Stories
layout: post
post-image: "https://iili.io/JiChI0g.png"
description: Tailormade microcopy to suit up your apps
tags:
  - Tech Specs
  - UX Design
  - UX Writing
  - Product Management
  - Technical Writing
  - English

---
## Use Case

🔥 ...

🍍 ...

🚀 ...

<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-J0NKP19PLY"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-J0NKP19PLY');
</script>

# Grant Managers Ability to Complete Routes

![intro](/assets/images/grant-manager-intro.png)

## On this Page
- [Goal](#goal)
- [Background and Strategic fits](#background-and-strategic-fits)
- [Requirements](#requirements)

## Goal
Allow Manager 7 users to execute **Route Actions** such as:
- **START ROUTE**
- **DEPART FROM ORIGIN**
- **CANCEL ALL STOPS**
- **ARRIVE AT DESTINATION**
- **COMPLETE ROUTE**

## Background and Strategic Fits
- Manager users usually come across a very common scenario where routes are not finished by their assigned drivers, and they need to take care of it. In doing so, they must contact a system administrator/dispatcher (i.e., Live users) and request them to complete such routes.
- The Manager application could become really handy if it allowed supervisors to execute all necessary route actions.

### Assumptions
- Manager users usually see themselves in the need of completing (closing) a route during service. This is due to several reasons, from the driver's GPS signal was lost or simply because they didn´t follow the right procedures.

## Requirements
### 1 - Add Route Actions Button at Route Details screen
#### User Story
As a Manager user, I would like to be able to access a section on the app where I can perform **Route Actions** available on **Live**.

#### Prototype
![image](/assets/images/grant-manager-1.png)

#### Acceptance Criteria
- **Route Actions** button must be available on every route's details.
- When tapping **Route Actions** button, the user must be redirected to **Route Actions** screen.

### 2 - Allow Manager Users to Cancel all Pending Stops and Arrive at the Warehouse
#### User Story
- As a Manager user, I would like to be able to execute **Arrive at the Warehouse** action on any route from my list.

#### Prototype
![image](/assets/images/grant-manager-2.png)
![image](/assets/images/grant-manager-3.png)
![image](/assets/images/grant-manager-4.png)

#### Acceptance Criteria
- When tapping **Route Actions** button, the user must be redirected to **Route Actions** screens.
- Route data must be displayed on top of the screen for an easier indentification (e.g., Route key, Status).
- **CONFIRM** button closes the screen and redirects the user to the **Route Detail** screen.
- **Statu** and **Actions** section must be displayed and reflecting actual route status.
- If current status is **ROUTE PROGRESS** then **ARRIVE AT DESTINATION** action button must be displayed.
- When tapping **ARRIVE AT DESTINATION** button, a modal must be displayed for the user input some necessary data:
- **Arrival at destination Date**
- **Cancel Reason**
- **Cancel**
- **Apply**
- If **CANCE**, then close action popup.
- If **APPLY**, then route status changes to **EQUIPMENT AT DESTINATION**.
- If **APPLY**, then current status will be **EQUIPMENT AT DESTINATION**, and **COMPLETE ROUTE** action button must be displayed.
- **SERVER ACTION**: In order to make this possible, **GMS** must authorise **GMM7** to use the following endpoints:<br>
`/Route/{routeID}/Stop/Cancel`<br>
`/Route/{routeID}/ArriveDestination/NoDriver`

### 3 - Allow Manager Users to Depart from Origin
#### User Story
- As a Manager user, I would like to be able to execute **Depart from Origin** action on any route from my list.

#### Prototype
![image](/assets/images/grant-manager-5.png)
![image](/assets/images/grant-manager-6.png)
![image](/assets/images/grant-manager-7.png)

#### Acceptance Criteria
- When tapping **Route Actions** button, the user must be redirected to **Route Actions** screens.
- Route data must be displayed on top of the screen for an easier indentification (e.g., Route key, Status). 
- **CONFIRM** button closes the screen and redirects the user to the **Route Detail** screen.
- **Status** and **Actions** section must be displayed and reflecting actual route status.
- If current status is **ROUTE-NOT-STARTED** then **START ROUTE** action button must be displayed.
- When tapping **START ROUTE** button, a modal must be displayed for the user input some necessary data: **Route Start Date> Start Driver Service Time (HOS)> Cancel> Apply**.
- If **CANCEL**, then close action popup.
- If **APPLY**, then route status changes to **STARTED**.
- If **APPLY**, then current status will be **EQUIPMENT AT ORIGIN**, and **DEPART FROM ORIGIN** action button must be displayed.
- **SERVER ACTION**: In order to make this possible, **GMS** must authorise **GMM7** to use the following endpoint:<br>
`/Route/{routeID}/Start`

### 4 - Allow Manager Users to Cancel all Pending Stops and Arrive at the Warehouse
#### User Story
- As a Manager user, I would like to be able to execute **Arrive at the Warehouse** action on any route from my list.

#### Prototype
![image](/assets/images/grant-manager-8.png)
![image](/assets/images/grant-manager-9.png)
![image](/assets/images/grant-manager-10.png)

#### Acceptance Criteria
- When tapping **Route Actions** button, the user must be redirected to **Route Actions** screens.
- Route data must be displayed on top of the screen for an easier indentification (e.g., Route key, Status).
- **CONFIRM** button closes the screen and redirects the user to the **Route Detail** screen.
- **Status** and **Actions** section must be displayed and reflecting actual route status.
- If current status is **ROUTE IN PROGRESS** then **ARRIVE AT DESTINATION** action button must be displayed.
- When tapping **ARRIVE AT DESTINATION** button, a modal must be displayed for the user input some necessary data:
- **Arrival at Destination Date**
- **Cancel Reason**
- **Cancel**
- **Apply**
- If **CANCEL**, then close action popup.
- If **APPLY**, then route status changes to **EQUIPMENT AT DESTINATION**.
- If **APPLY**, then current status will be **EQUIPMENT AT DESTINATION**, and **COMPLETE ROUTE** action button must be displayed.
- **SERVER ACTION**: In order to make this possible, **GMS** must authorise **GMM7** to use the following endpoints:<br>
`/Route/{routeID}/Stop/Cancel`<br>
`/Route/{routeID}/ArriveDestination/NoDriver`

### 5 - Allow Manager Users to Complete a Route
#### User Story
- As a Manager user, I would like to be able to execute **Complete Route** action on any route from my list.

#### Prototype
![image](/assets/images/grant-manager-11.png)
![image](/assets/images/grant-manager-12.png)
![image](/assets/images/grant-manager-13.png)

#### Acceptance Criteria
- When tapping **Route Actions** button, the user must be redirected to **Route Actions** screen.
- Route data must be displayed on top of the screen for an easier indentification (e.g., Route key, Status)
- **CONFIRM** button closes the screen and redirects the user to the **Route Detail** screen.
- **Status** and **Actions** section must be displayed and reflecting actual route status.
- If current status is **EQUIPMENT AT DESTINATION** then **COMPLETE ROUTE** action button must be displayed.
- When tapping **COMPLETE ROUTE** button, a modal must be displayed for the user input some necessary data:
- **Complete Route Date**
- **Driver**
- **Cancel**
- **Apply**
- If **CANCEL**, then close action popup.
- If **APPLY**, then route status changes to **ROUTE COMPLETED**.
- **SERVER ACTION**: In order to make this possible, **GMS** must authorise **GMM7** to use the following endpoint:<br>
`/Route/{routeID}/Complete`

## User Interaction and Design
The following details describe user interaction and the specifics of each screen. The images may contain links that lead to the [interactive prototype](https://xd.adobe.com/view).
<br>

[Back to Home Page](/)