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
# DoxHut SDK Documentation

The DoxHut SDK is a powerful library designed to facilitate seamless integration between the iSales application used in Pepsico Russia's operation and the DoxHut system. By leveraging the DoxHut SDK methods, users can efficiently manage routes, initiate route plans, and complete routes directly from the iSales app. This documentation provides an in-depth guide to utilizing the DoxHut SDK and its key functionalities.

![intro](/assets/images/images-sdk-driver-flow.png)

## DoxHut SDK - Library - Methods

**Goal**

- Build an API to integrate with iSales in Pepsico Russia's operation.

**Background and Strategic Fits**

Currently, Pepsico Russia's drivers use the iSales application to manage their routes and perform delivery-related activities. The goal is to import the routes from SAP into DoxHut, while the users continue to utilize the iSales app.

**Assumptions**

- iSales users will continue to use the application, while the routes will be imported into DoxHut.

**Requirements**

- Build an API to integrate with iSales in Pepsico Russia's operation.

**GM Driver 7 Flow**

[Flowchart illustrating the entire driver routing]

## DoxHut SDK - Methods - Start Route

**Goal**

- Start a route from a host application on the DoxHut Server via the DoxHut Engine.

**Background and Strategic Fits**

- On Pepsico Russia operation, routes are currently departed from origin on iSales app.
- Currently routes are imported from SAP into iSales.

**Assumptions**

- Routes will be imported from SAP to DoxHut and will contain all necessary information for successful loading on both the host app and DoxHut Engine.
- System administrators will set up and maintain the driver's configurations on DoxHut Live, such as permissions and restrictions of route actions.

**Requirements**

- Make it possible for Pepsico Russia drivers to start routes from a host app to the DoxHut Server via the DoxHut Engine.

| Title | User Story | DoxHut Engine Method | Flow | Acceptance Criteria |
| --- | --- | --- | --- | --- |
| Start Route | As an iSales user from Pepsico RU's operation, I need to be able to start routes. | DoxHutEngine.startRoute | Success Scenario 1 - Successfully start route
It is called DoxHutEngine.startRoute with success
Requirements:
• The driver must have loaded the route previously.
• The driver must not have started the route previously.
Failure Scenario 1 - Network error
It is called DoxHutEngine.startRoute, then NetworkErrorException.
Requirements:
• It must be able to communicate with the server.
Failure Scenario 2 - No route loaded
It is called DoxHutEngine.startRoute, then NoRouteLoadedException.
Requirements:
• It must be able to communicate with the server.
• The driver must not have loaded the route previously.
Failure Scenario 3 - Route already started
It is called DoxHutEngine.startRoute, then RouteAlreadyStartedException.
Requirements:
• It must be able to communicate with the server.
• The driver must have loaded the route previously.
• The driver must not have started the route previously. | • Verify if the route status changes to STARTED after executing the start route action.
• Verify if any other route changes its status to STARTED after the execution of this action.
• Verify that this method uses the Request Queue properly. |

## DoxHut SDK - Methods - Complete Route

**Goal**

- Complete routes from a host application on the DoxHut Server via the DoxHut Engine.

**Background and Strategic Fits**

- On Pepsico Russia operation, routes are currently departed from origin on iSales app.
- Currently routes are imported from SAP into iSales.

**Assumptions**

- Routes will be imported from SAP to DoxHut and will contain all necessary information for successful loading on both the host app and DoxHut Engine.
- System administrators will set up and maintain the driver's configurations on DoxHut Live, such as permissions and restrictions of route actions.

**Requirements**

- Make it possible for Pepsico Russia drivers to complete routes from a host app to the DoxHut Server via the DoxHut Engine.

| Title | User Story | DoxHut Engine Method | Flow | Acceptance Criteria |
| --- | --- | --- | --- | --- |
| Complete Route | As an iSales user from Pepsico RU's operation, I need to be able to inform the DoxHut Engine when I complete a route. | DoxHutEngine.completeRoute | Success Scenario 1 - It is called DoxHutEngine.completeRoute with success
Requirements:
• The driver must have previously executed the Arrive at Destination method.
• It must be able to communicate with the server.
• The driver must have loaded the route previously.

Failure Scenario 1 - Network error
It is called DoxHutEngine.completeRoute, then NetworkErrorException is thrown.
Requirements:
• It must not be able to communicate with the server.

Failure Scenario 2 - No route loaded
It is called DoxHutEngine.completeRoute, then NoRouteLoadedException is thrown.
Requirements:
• It must be able to communicate with the server.
• The driver must not have loaded the route previously.

Failure Scenario 3 - Still not arrived at the destination
It is called DoxHutEngine.completeRoute, then StillNotArrivedAtDestination is thrown.
Requirements:
• The driver must have not previously executed the Arrive at Destination method.
• It must be able to communicate with the server.
• The driver must have loaded the route previously. | • Verify if the route status changes to COMPLETED after executing the complete route action.
• Verify if any other route changes its status to COMPLETED after the execution of this action.
• Make sure it is not possible to complete the route without having previously executed the Arrive at Destination method. |


![2023-07-00-929092.png](https://naguipinetta.github.io/assets/2023-07-00-929092.png)
