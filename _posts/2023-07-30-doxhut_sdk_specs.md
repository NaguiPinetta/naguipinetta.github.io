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

# <span style="color: #00008B">DoxHut SDK Specification</span>

## <span style="color: #000000">Introduction</span>

- Currently, <span style="color: #00008B">pepsico-ru</span> drivers utilize the <span style="color: #00008B">iSales</span> mobile application to manage their routes and handle delivery-related tasks. To streamline their operations and enhance efficiency, we aim to integrate their existing <span style="color: #A52A2A">ERP</span> route import solution with <span style="color: #00008B">DoxHut</span>. To achieve this, we will create a robust API structure that facilitates seamless integration between their <span style="color: #A52A2A">ERP</span> system and <span style="color: #00008B">DoxHut</span>.

- Additionally, we will develop a <span style="color: #00008B">DoxHut SDK</span>, which will enable their <span style="color: #00008B">iSales</span> app to interact with specific endpoints on the <span style="color: #00008B">DoxHut API</span>.
<br>
<br>
### <span style="color: #006400">DoxHut Driver Flow</span>

![intro](/assets/images/images-sdk-driver-flow.png)

## <span style="color: #000000">DoxHut SDK - Library - Methods</span>

### <span style="color: #000000">Start Route</span>

**Goal**<br>
<br>
- Start a route from a host application on the <span style="color: #00008B">DoxHut Server</span> via the <span style="color: #00008B">DoxHut Engine</span>.

**Background and Strategic Fits**<br>
<br>
- On <span style="color: #00008B">pepsico-ru</span>, routes are currently initiated from the origin using the <span style="color: #00008B">iSales</span> app.
- Currently, routes are imported from <span style="color: #A52A2A">ERP</span> into <span style="color: #00008B">iSales</span>.

**Assumptions**<br>
<br>
- Routes will be imported from <span style="color: #A52A2A">ERP</span> to <span style="color: #00008B">DoxHut</span>, containing all necessary information for successful loading on both the host app and <span style="color: #00008B">DoxHut Engine</span>.
- System administrators will configure and maintain driver configurations, permissions, and route action restrictions on <span style="color: #00008B">DoxHut Live</span>.
<br>
<br>
#### <span style="color: #A52A2A">Requirements</span>

- Make it possible for <span style="color: #00008B">Pepsico RU</span> drivers to start routes from a host app to the <span style="color: #00008B">DoxHut Server</span> via the <span style="color: #00008B">DoxHut Engine</span>.
<br>
<br>
#### <span style="color: #A52A2A">User Story</span>

- As an <span style="color: #00008B">iSales</span> user from <span style="color: #00008B">Pepsico RU</span>'s operation, I need to be able to start routes.
<br>
<br>
#### <span style="color: #A52A2A">DoxHut Engine Method</span>

- Starts the route loaded by the user and changes its status to <span style="color: #A52A2A">"in progress"</span>.

**Throws:**
- <span style="color: #A52A2A">TenantNotDefinedException</span> when no tenant has been informed.
- <span style="color: #A52A2A">NoRouteLoadedException</span> when no route has been loaded.
- <span style="color: #A52A2A">RouteAlreadyStartedException</span> when the route has already been started.
- <span style="color: #A52A2A">NetworkErrorException</span> when it was not possible to establish communication with the server.
<br>
<br>
> <span style="color: #00008B">Note</span>: Communication interruptions, lack of connectivity, or when the server is down may cause <span style="color: #A52A2A">NetworkErrorException</span>.

##### <span style="color: #A52A2A">Flow</span>

###### <span style="color: #8B0000">Success Scenario 1 - Successfully start route</span>

- <span style="color: #00008B">DoxHutEngine.startRoute</span> is called successfully.

**Requirements:**<br>
<br>
- Communication with the server.
- The driver must have previously loaded the route.
- The route could not have been previously started.
<br>
<br>
###### <span style="color: #8B0000">Failure Scenario 1 - Network error</span>

- <span style="color: #00008B">DoxHutEngine.startRoute</span> is called, then <span style="color: #A52A2A">NetworkErrorException</span> is thrown.

**Requirements:**<br>
<br>
- Communication with the server.
<br>
<br>
###### <span style="color: #8B0000">Failure Scenario 2 - No route loaded</span>

- <span style="color: #00008B">DoxHutEngine.startRoute</span> is called, then <span style="color: #A52A2A">NoRouteLoadedException</span> is thrown.

**Requirements:**<br>
<br>
- Communication with the server.
- The driver must not have previously loaded the route.
<br>
<br>
###### <span style="color: #8B0000">Failure Scenario 3 - Route already started</span>

- <span style="color: #00008B">DoxHutEngine.startRoute</span> is called, then <span style="color: #A52A2A">RouteAlreadyStartedException</span> is thrown.

**Requirements:**<br>
<br>
- Communication with the server.
- The driver must have previously loaded the route.
- The route could not have been previously started.
<br>
<br>
##### <span style="color: #A52A2A">Acceptance Criteria</span>

- Verify whether the route status changes to <span style="color: #A52A2A">STARTED</span> after executing the start route action.
- Verify whether any other route changes its status to <span style="color: #A52A2A">STARTED</span> after executing this action.
- Verify whether this method uses the <span style="color: #A52A2A">Request Queue</span> correctly.
<br>
<br>
### <span style="color: #000000">Complete Route</span>

**Goal**<br>
<br>
- Complete routes from a host application on the <span style="color: #00008B">DoxHut Server</span> via the <span style="color: #00008B">DoxHut Engine</span>.

**Background and Strategic Fits**<br>
<br>
- On <span style="color: #00008B">pepsico-ru</span> operation, routes are currently departed from the origin using the <span style="color: #00008B">iSales</span> app.
- Currently, routes are imported from <span style="color: #A52A2A">ERP</span> into <span style="color: #00008B">iSales</span>.

**Assumptions**<br>
<br>
- Routes will be imported from <span style="color: #A52A2A">ERP</span> to <span style="color: #00008B">DoxHut</span>, containing all necessary information for successful loading on both the host app and <span style="color: #00008B">DoxHut Engine</span>.
- System administrators will configure and maintain driver configurations, permissions, and route action restrictions on <span style="color: #00008B">DoxHut Live</span>.
<br>
<br>
#### <span style="color: #A52A2A">Requirements</span>

- Make it possible for <span style="color: #00008B">pepsico-ru</span> drivers to complete routes from a host app to the <span style="color: #00008B">DoxHut Server</span> via the <span style="color: #00008B">DoxHut Engine</span>.
<br>
<br>
#### <span style="color: #A52A2A">User Story</span>

- As an <span style="color: #00008B">iSales</span> user from <span style="color: #00008B">pepsico-ru</span>'s operation, I need to be able to inform the <span style="color: #00008B">DoxHut Engine</span> when I complete a route.
<br>
<br>
#### <span style="color: #A52A2A">DoxHut Engine Method</span>

- Action input by the driver or system administrator to indicate the route has been completed.
<br>
<br>
> <span style="color: #00008B">Note</span>: This is the last route action possible and can only be performed once the driver arrived at the destination and all stops are in a status different than <span style="color: #A52A2A">"pending"</span>.

**Throws:**
- <span style="color: #A52A2A">TenantNotDefinedException</span> when no tenant has been informed.
- <span style="color: #A52A2A">StillNotArrivedAtDestination</span> when the action <span style="color: #A52A2A">"Arrive at Destination"</span> has not yet been performed.
- <span style="color: #A52A2A">NoRouteLoadedException</span> when no route has been loaded.
- <span style="color: #A52A2A">NetworkErrorException</span> when it was not possible to establish communication with the server.
<br>
<br>
> <span style="color: #00008B">Note</span>: Communication interruptions, lack of connectivity, or when the server is down may cause <span style="color: #A52A2A">NetworkErrorException</span>.
<br>
<br>
#### <span style="color: #A52A2A">Flow</span>

##### <span style="color: #8B0000">Success Scenario 1 - It is called DoxHutEngine.completeRoute with success</span>

**Requirements:**
- The driver must have previously executed the <span style="color: #A52A2A">Arrive at Destination</span> method.
- Communication with server.
- The driver must have previously loaded the route.
<br>
<br>
##### <span style="color: #8B0000">Failure Scenario 1 - Network error</span>

- <span style="color: #00008B">DoxHutEngine.completeRoute</span> is called, then <span style="color: #A52A2A">NetworkErrorException</span> is thrown.

**Requirements:**
- It must not be able to communicate with the server.
<br>
<br>
##### <span style="color: #8B0000">Failure Scenario 2 - No route loaded</span>

- <span style="color: #00008B">DoxHutEngine.completeRoute</span> is called, then <span style="color: #A52A2A">NoRouteLoadedException</span> is thrown.

**Requirements:**
- Communication with server.
- The driver must not have previously loaded the route.
<br>
<br>
##### <span style="color: #8B0000">Failure Scenario 3 - Still not arrived at the destination</span>

- <span style="color: #00008B">DoxHutEngine.completeRoute</span> is called, then <span style="color: #A52A2A">tillNotArrivedAtDestination</span> is thrown.

**Requirements:**
- The driver must not have previously executed the <span style="color: #A52A2A">Arrive at Destination</span> method.
- Communication with server.
- The driver must have previously loaded the route.
<br>
<br>
#### <span style="color: #A52A2A">Acceptance Criteria</span>

- Verify whether the route status changes to <span style="color: #A52A2A">COMPLETED</span> after executing the complete route action.
- Verify whether any other route changes its status to <span style="color: #A52A2A">COMPLETED</span> after executing this method.
- Ensure it is not possible to complete the route without having previously executed the <span style="color: #A52A2A">Arrive at Destination</span> method.

[Back to Home Page](/)
