---
title: DoxHut SDK Specs

---
# DoxHut SDK Documentation

The DoxHut SDK is a powerful tool designed to seamlessly integrate DoxHut driver applications and the backend server with Pepsico Russia's iSales solution. It provides a set of methods that enable efficient route planning, initiation, and completion directly from the iSales app. By leveraging the DoxHut SDK, drivers can effortlessly manage routes, ensuring accurate and real-time data exchange between the iSales app and the DoxHut Server.

## GreenMile Nav - Permit Receiving Configurations via Intent

**Meta**

- Allow other applications to send vehicle configurations, route restrictions, and hazardous materials load to the DoxHut Nav.

**Premises**

- Currently, the configurations are manually set by the driver (Driver 7 user).
- Along the route, both the material load and vehicle weight may change. An external application could send updated vehicle specs to take advantage of different scenarios, relieving the driver of this responsibility and making the configurations more dynamic and aligned with reality.

**Requirements**

- Add a stop from a host application on the DoxHut Server via the DoxHut Engine.

| Req | User Story | GM Engine Method | Flow | Acceptance Criteria |
| --- | --- | --- | --- | --- |
| 01 | As a user of DoxHut Nav, I want to avoid manual app configurations by receiving them directly from the last-mile application I use. | GMEngine.addStop | Success Scenario 1 - Successfully Add Stop
• It is called GMEngine.addStop with success
Requirements:
• it must be able to communicate with the server
• the driver must have started the route previously
Failure Scenario 1 - Network Error
• It is called GMEngine.addStop then NetworkErrorException.
Requirements:
• it must not be able to communicate with the server
Failure Scenario 2 - Route Not Started
• It is called GMEngine.addStop then RouteNotStartedException.
Requirements:
• it must be able to communicate with the server
• the driver must not have started the route previously. | • Verify if the stop is created and added to the route.
• Verify if the added stop has all necessary information and its position on the route is correct. |

## GreenMile SDK - Methods - Start Route

**Goal**

- Start a route from a host application on the DoxHut Server via the DoxHut Engine.

**Background and Strategic Fits**

- On Pepsico Russia's operation, routes are currently departed from the origin on the iSales app.
- Currently, routes are imported from SAP into iSales.

**Assumptions**

- Routes will be imported from SAP to DoxHut and will contain all necessary information for successful loading on both the host app and DoxHut Engine.
- System administrators will set up and maintain the driver's configurations on DoxHut Live, such as permissions and restrictions of route actions.

**Requirements**

- Make it possible for Pepsico Russia drivers to start routes from a host app to the DoxHut Server via the DoxHut Engine.

| Title | User Story | GM Engine Method | Flow | Acceptance Criteria |
| --- | --- | --- | --- | --- |
| Start Route | As an iSales user from Pepsico RU's operation, I need to be able to start routes. | GMEngine.startRoute | Success Scenario 1 - Successfully start route
It is called GMEngine.startRoute with success
Requirements:
• the driver must have previously executed the Arrive at Destination method.
• it must be able to communicate with the server.
• the driver must have loaded the route previously

Failure Scenario 1 - Network Error
It is called GMEngine.startRoute then NetworkErrorException is thrown.
Requirements:
• it must not be able to communicate with the server
Failure Scenario 2 - No Route Loaded
It is called GMEngine.startRoute then NoRouteLoadedException is thrown.
Requirements:
• it must be able to communicate with the server.
• the driver must not have loaded the route previously
Failure Scenario 3 - Route Already Started
It is called GMEngine.startRoute then RouteAlreadyStartedException is thrown.
Requirements:
• it must be able to communicate with the server.
• the driver must have loaded the route previously.
• the driver must not have started the route previously. | • Verify if route status changes to STARTED after executing the start route action.
• Verify if any other route changed their status to STARTED after the execution of this action.
• Verify that this method uses the Request Queue properly. |

## GreenMile SDK - Methods - Complete Route

**Goal**

- Complete routes from a host application on the DoxHut Server via the DoxHut Engine.

**Background and Strategic Fits**

- On Pepsico Russia's operation, routes are currently departed from the origin on the iSales app.
- Currently, routes are imported from SAP into iSales.

**Assumptions**

- Routes will be imported from SAP to DoxHut and will contain all necessary information for successful loading on both the host app and DoxHut Engine.
- System administrators will set up and maintain the driver's configurations on DoxHut Live, such as permissions and restrictions of route actions.

**Requirements**

- Make it possible for Pepsico Russia drivers to complete routes from a host app to the DoxHut Server via the DoxHut Engine.

| Title | User Story | GM Engine Method | Flow | Acceptance Criteria |
| --- | --- | --- | --- | --- |
| Complete Route | As an iSales user from Pepsico RU's operation, I need to be able to inform the GM Engine when I complete a route. | GMEngine.completeRoute | Success Scenario 1
It is called GMEngine.completeRoute with success
Requirements:
• the driver must have previously executed the Arrive at Destination method.
• it must be able to communicate with the server.
• the driver must have loaded the route previously

Failure Scenario 1 - Network Error
It is called GMEngine.completeRoute then NetworkErrorException is thrown.
Requirements:
• it must not be able to communicate with the server
Failure Scenario 2 - No Route Loaded
It is called GMEngine.completeRoute then NoRouteLoadedException is thrown.
Requirements:
• it must be able to communicate with the server.
• the driver must not have loaded the route previously
Failure Scenario 3 - Still Not Arrived at Destination
It is called GMEngine.completeRoute then StillNotArrivedAtDestination is thrown.
Requirements:
• the driver must have not previously executed the Arrive at Destination method.
• it must be able to communicate with the server.
• the driver must have loaded the route previously | • Verify if route status changes to COMPLETED after executing the complete route action.
• Verify if any other route changed their status to COMPLETED after the execution of this action.
• Make sure it is not possible to complete the route without having previously executed the Arrive at Destination method. |

By leveraging the DoxHut SDK and its methods, Pepsico Russia can streamline its route management processes and optimize its delivery operations, enhancing overall efficiency and customer satisfaction.

Please note that the provided documentation is subject to updates and improvements to meet specific use cases and requirements. For any questions or support, feel free to contact our team.

---
This is the revised and expanded introduction for the combined documentation page, now titled "DoxHut SDK Documentation." If you need further modifications or have any specific preferences, don't hesitate to let me know!

![2023-07-00-929092.png](https://naguipinetta.github.io/assets/2023-07-00-929092.png)
