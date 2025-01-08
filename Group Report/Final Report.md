<!---

---
title: "CASA0017: Web Architecture Final Assessment"
author: Jiaying shen"
date: "8 Jan 2025"
---

-->
# London Tube Planner 
<small>Jiaying Shen</small>



---
## Introduction

Tetro, C. (2023) mentioned London has the world's oldest underground transport system. The tube offers a fast, zone-spanning alternative to congested road traffic, and its waiting times are generally predictable. However, determining the optimal time to travel between locations and for people who do not familiar with tube can be challenging.

Consider a scenario in which a student has a class starting in one hour. She arrives at the tube station as usual, only to discover that the line is temporarily closed. In such cases, is it feasible for her to switch to another mode of transport and still arrive on time? This situation highlights a common issue: passengers often only become aware of delays or closures after arriving at the station. Salisbury, J. et al. (2024) noted that the London tube system occasionally experiences signal prohibitions or machine breakdowns, leading to minor delays or temporary closures. Although various pieces of information are available at tube stations, such as the operational status of different lines at the entrance, platform details after passing through the gate, and estimated train arrival times while waiting. These information is typically fragmented and scattered across different points in the station. Integrating these details into a unified platform could help passengers plan their journeys more effectively, reducing stress and enhancing the overall commuting experience.

With the current technology, the TfL Journey Planner performs a similar function. However, the London Tube Planner focuses on providing deeper insights into the Tube network. It achieves this through a map-based interface and offers more interactive features to display real-time Tube transportation data.

---
## Website Design Overview

![](https://raw.githubusercontent.com/JY-SHENNNN/casa0017-web-assessment/refs/heads/main/Group%20Report/src/website%20layout.png)

The design process begins with creating the website layout. From a personal perspective, the website should visualize the tube lines with detailed station names and include interactive features such as selectable dropdown boxes. Additionally, the site integrates service status information, estimated tube arrival times, and train destinations. The final layout is shown above.

## Development process
![](https://raw.githubusercontent.com/JY-SHENNNN/casa0017-web-assessment/refs/heads/main/Group%20Report/src/flowchart.png)
The development starts by coding the `index.html` and `style.css` files. The main `div` elements divide the page into three sections, to ensure better organization and application in later stages. Basic layout properties such as width, height, padding, and background color are set in `style.css` to ensure a clean and structured interface. The core functionality focuses on visualizing tube lines and stations on the map. Initially, Google Maps is used, as demonstrated in workshops, by integrating the Google Maps API to load the map seamlessly.

#### Visualization of Lines and Stations

To display markers and lines on the map, accurate latitude and longitude data are required. The TfL (Transport for London) API is utilized to retrieve branch and station data for each tube line. By iterating through the latitude and longitude of each station, the coordinates are stored in a collection to eliminate duplicates and preserve the branch paths. Google Maps Polyline is used to draw the tube line branches on the map, while stations are marked with circular markers using the Marker class. To enhance interactivity, event listeners are added to the markers, allowing an info box to appear when the user hovers over a station. This displays details such as the station name, latitude, and longitude. Additionally, lines are highlighted when hovered over, providing a more interactive and intuitive experience. This is achieved by cloning the existing map layer, modifying the stroke width or marker size, and re-rendering the visualization.

#### Line Visualization on line.html

The second page (line.html) follows a similar process. When the page loads, the line ID is extracted from the URL, and the TfL API is queried to obtain the route and stop point details for the selected line. Polylines are drawn to represent the branches, while circular markers display the station locations. This ensures that users can view a comprehensive visualization of the entire tube line. Google Maps provides powerful visualization tools, but public deployment can lead to security risks, especially with API key exposure. Handling large numbers of markers and polylines can also affect performance. Deck.GL addresses these issues by offering high performance without the need for API keys. Thus, Deck.GL is used to display the lines and stations through `ScatterplotLayer` and `LineLayer` components with exactly same implementation idea. 

#### Key challenge and solution:
The main challenge was incomplete API data and incorrect calls, leading to missing information. For example, discrepancies between the Hammersmith & City line’s id and name caused errors when querying Naptan codes. This issue was resolved by using `console.log` to trace the parameters passed into the API and identify the correct endpoints. Additionally, bus, tube, and train stations share names but have different Naptan codes, which caused incorrect message returned. By inspecting API responses and using browser developer tools, the appropriate codes for tube mode can be obtained correctly.

Another key issue involved is timing conflict between `asynchronous` (async) and `synchronous` (sync) functions, which caused incomplete map loading and visualization. Implementing `await` ensured proper execution order. Visualization problems also occurred when layers in Deck.GL were rendered in the wrong order, causing some lines or markers to be hidden beneath others. Adjusting the layer hierarchy resolved this, ensuring that all elements displayed correctly. Through consistent debugging and careful API data handling, the final visualization became smooth and accurate. 

## Reflection and conclusion
This project focuses on the front-end only, but the multiple API calls resulted in slow website loading. Additionally, unstable API connections sometimes led to invalid data returns. Dividing the project into back-end and front-end components could potentially resolve this issue. The lack of a function to encapsulate duplex functionality for multiple uses cost me considerable time for debugging and revising. From the user's perspective, future development could include features like a route planner, estimated travel time between start and destination stations, and enhanced crowding data visualization. Also, the current main page design could be improved due to overlapping stations. Throughout the project, ideas frequently emerged after completing each part. For example, after loading the map, I realized the need to visualize the lines and stations. Once those were visualized, I thought about increasing interactivity to make it easier for users to access information. In the meanwhile, the decision made before the project is quite important to save and manage time. The iterative process and debugging were quite enjoyable. 

This project aims to provide real-time tube information to help users plan their travel time efficiently. Its interactive interface and clear presentation of information assist users in making decisions quickly. Furthermore, it encourages more people to use the tube, helping to reduce traffic congestion and save time.


## Biblography

1. Tetro, C. (2023). Mind the Gap: Traveler Tips for Riding the Tube in London. <https://montagetravel.com/riding-the-tube-in-london/>

2. Salisbury, J. et al. (2024). London travel news LIVE: Tube and Overground meltdown as TfL network hit by suspensions and delays. <https://www.standard.co.uk/news/london/travel-updates-latest-tube-closures-london-underground-overground-trains-tfl-b1192824.html>


----

## Declaration of Authorship

I, Jiaying Shen, confirm that the work presented in this assessment is my own. Where information has been derived from other sources, I confirm that this has been indicated in the work.


Digitally Sign with Your name Here

ASSESSMENT DATE
