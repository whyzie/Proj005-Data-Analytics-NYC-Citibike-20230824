# Proj005-Data-Analytics-NYC-citibike-20230824
<img style="float:left" src="https://i.imgur.com/DWQOJgU.png" width="1500">

<h1 style="text-alignment:justify">NYC Citibike Trips</h1>
<hr>
24 Aug 2023
<div>
<img style="float: left" src="https://i.postimg.cc/qvZpHzhk/002-Img-Objectives-Draft-2-20220819.png(https://postimg.cc/cvYpQ1Bj)" width="75">
<h2 id="Obj1">Objectives</h2>
<hr>

<h3 style="text-align:justify">In this project, we will walk through the Data Analytics process, starting from data acquisition and analysis, to gaining business insights and creating models using BigQuery with SQL and Python. The case study will showcase data analyst, business intelligence, and data science analyses to acquire valuable business insights.
<br><br>
The New York Citibike Cyclistic's Customer Growth Team is developing a business plan for the next year (2016). Therefore, the case study will only utilize data from 2014 and 2015. The team's primary objective is to understand how their customers are using their bikes, with a focus on identifying customer demand at different station locations. The key question is: How can we apply customer usage insights to inform new station growth?<br><br>
After part 1 (P01) we have cleaned the data and in part 2 (P02), executed data mining and analysis. Now in part 3 (P03), we will continue creating predictive models on the demand side. The goal of data mining is to gain a deeper understanding of the data and to use this knowledge to make informed decisions, create predictive models, or find valuable patterns and trends for valuable insights. <b>Develop machine learning models that predicts citibike total trip or trip durations based on location and time of day.</b>
</h3> 
<p style = "font-family: Arial; font-size: 18px">Note: This project's dataset was created for pedagogical purposes and may not represent real-world data. The project consists of multiple notebook parts, focusing on combining data from various tables and conducting data analysis and prediction to acquire valuable insights.</p>    
</div> 

# Understanding the price structure

#### Pricing to determine revenue

<ul style ="font-family:Verdana; font-size:16px; text-align:justify">
    <li>Annual Citi Bike memberships cost \$149 (\$99 at launch) and provide members with an unlimited number of 45-minute rides.
<li>Rides longer than 45 minutes result in overage charges ranging from \$2.50 for an additional 25 minutes to more than \$9.00 for additional time.
<li>Seven-day passes are available for \$25 with similar trip time constraints.
<li>24-hour passes are available for \$9.95, both with similar trip time constraints.
<li>Bikes that are missing for longer than 24 hours can result in a /$1,200 fee (plus tax) charged to the account holder that took out the bike.
<li>New York City Housing Authority residents and credit union members qualify for discounted \$60 annual memberships.</ul>

<p style ="font-family:Verdana; font-size:16px; text-align:justify">The pricing system was established in 2013 with the intention that one-day and seven-day passes for casual users would provide a subsidy for the \$95 annual membership offered to subscribers. In addition to user-generated revenue, Citibike also generated income through sponsorships. Notably, Citibank, the program's primary advertising sponsor, agreed to extend its licensing deal from the original end date in 2019 to 2024. This extension resulted in an additional \$70.5 million being added to its initial sponsorship.</p>
<p style ="font-family:Verdana; font-size:16px; text-align:justify">After a period of declining performance in 2014 compared to 2013, the CEO took action for improvements in 2015. Citibike hired 28 new employees to bolster the corporate team. On the operational front, the company introduced a tracking app to monitor users' trips. By August 2015, a new back-end operating system had been implemented, older kiosks were swapped out for new ones, and approximately 12,000 docking points were either replaced or repaired. Moreover, 134 additional stations were installed, coinciding with the company's rebranding from Alta Bikeshare Systems to Motivate.
<br><br>
Citi Bike also unveiled a new bike model, which closely resembles the previous version but offers enhanced functionality. Around 2,400 of these new bikes were deployed throughout New York City.
<br><br>
In terms of maintenance, the repairs team implemented weekend shifts and conducted more on-street repairs, reducing the need to bring bikes back to the shop. Furthermore, a proactive approach was adopted for stations with low batteries; these were identified and replaced before causing service disruptions. This strategy aimed to prevent malfunctions rather than responding to unusable stations after the fact.</p>
<p style ="font-family:Verdana; font-size:16px; text-align:justify">In order to create business plan for 2016 it is important to have a complete overview about Citibike up to the latest.</p>

<div class="alert alert-block alert-warning">
<img style="float: left" src="https://i.postimg.cc/kXz8cFqC/005-Img-Yellow-Notes-Draft-1-20220819.png" width="60">
<b style = "font-family: Arial; font-size: 16px">Please note:</b><p style = "font-family:Verdana; font-size:14px"><b>Due to our lack of precise information regarding the quantities of each user type, new versus existing customers, as well as the specific breakdown of revenue from user types, sponsorships, and bike categories, we are currently unable to perform accurate revenue calculations and a comprehensive analysis of the revenue sources. Our dependable data sources include trip records and average trip durations. It's important to note that we have chosen not to include a competitor analysis, which would involve assessing comparable systems like Citibikes in other states or alternative modes of transportation.</b><p>
</div>

<div class="alert alert-block alert-warning">
<img style="float: left" src="https://i.postimg.cc/kXz8cFqC/005-Img-Yellow-Notes-Draft-1-20220819.png" width="60">
<b style = "font-family: Arial; font-size: 16px">Please note:</b><p style = "font-family:Verdana; font-size:14px">As we analyze the data, we observe that in September 2014, the highest recorded trip count was 8,361, indicating the utilization of 4,363 bikes. Similarly, September 2015 saw 10,546 trips with 5,396 bikes in use. Membership has experienced significant growth, with figures climbing from around 89,296 in October 2014 to surpassing 120,000 members by 2015. The bike count has also increased from 6,000 in 2013 to 7,454 by September 2015. A crucial question arises: "Do we require more bikes?"
    <br>Delving into calculations, if we target a daily trip count of 9,000 trips per month in 2014 (peak in September), this translates to 300 trips daily. Consequently, a minimum of 3,000 bikes appears sufficient for the year. If we further break this down to an hourly basis—300 trips per day over 20 hours—we find that around 15 trips per hour per bike are needed. Utilizing the average time data, this implies that approximately 15 bikes per hour suffice. Considering a safety stock for backup bikes (given a lack of repair data), let's assume 30 bikes per hour, culminating in 600 bikes per day. This count stands twice as high as the actual data recorded in September 2014.
    <br>
    <b>Hence, while we possess a membership base of nearly 90,000 in October 2014, the trip data only reflects around 9,000 trips. This discrepancy underscores the necessity of user ID tracking to ascertain how many registered members are actively utilizing the bike-sharing service. Despite having close to 90,000 registered members, the actual trip count remains considerably lower, prompting a closer examination of user engagement and the factors affecting it.</b>
  <p>
</div>

# Define the Process
<hr>

## Voice of Customers (VoC)
<img style="display: block; margin: 0 auto;" src="https://i.imgur.com/ftF6Pps.png" width="750">
<div style = "font-family: Arial; font-size: 16px">
    To measure neighborhood awareness, perceptions, and experience with Citi Bike, Restoration, in partnership with DOHMH, developed an intercept survey over the summer 2015.The survey findings revealed that a significant majority of individuals in Bedford Stuyvesant (87%) were familiar with Citi Bike. However, only a minority of respondents (18%) had utilized the service. Surprisingly, nearly one third (32%) expressed disagreement with the notion that Citi Bike was "intended for people like me," despite a significant proportion (74%) indicating their preference for having a Citi Bike station near to their residences. Additionally, only 36% of residents reported cycling within the past year. Notably, there was minimal awareness (9%) of the pre-existing discounted annual membership option available to NYCHA residents.
</div>

<table style="color:black;
           display:fill;
           border-colapse: colapse;
           width: 100%;
           border: 1px solid black;
           border-collapse: collapse;
           border-style: solid;
           border-radius:5px;
           background-color:#5642C5;
           font-size:110%;
           font-family:Verdana;
           letter-spacing:0.5px">
  <h3 style = "text-align:center">Table 1.1. SIPOC Analysis</h3>
  <tr>
    <th>Supplier (S)
    <th colspan="2">Input (I)</th>    
    <th colspan="4">Process (P)</th>
    <th colspan="2">Output (O)</th>
    <th colspan="2">Customer (C)</th>  
  </tr>
    <td>Citibike kiosk
    <br>Apps</td>
    <td colspan="2">Rent
        <ul>
            <li>Master card
            <li>Payment receipt
            <li>Key by inputing the pass code number or apps by scanning QR codes or inputing vehicle ID Number in apps. 
            <li>Bike park out and lock out(classic bikes and e-bikes)
        </ul></td> 
    <td style="background:LightSkyBlue;text-align:center">Pay for rent through kiosk or mobile apps</td>
    <td style="background:LightSkyBlue;text-align:center">Unlock it</td>
    <td style="background:LightSkyBlue;text-align:center">Ride it</td>
    <td style="background:LightSkyBlue">Park it </td>
    <td colspan="2" style="margin: auto; display:fill; word-wrap: break-word">
        <ul>
            <li>Travel report
            <li>Bike park in and lock in
        </ul>
    </td>
    <td colspan="2" style="margin: auto; display:fill; word-wrap: break-word">
        <ul>
            <li>Rider
            <li>Open dock in any station
        </ul>
    </td>
 </table>
<div class="alert alert-block alert-warning">
<img style="float: left" src="https://i.postimg.cc/kXz8cFqC/005-Img-Yellow-Notes-Draft-1-20220819.png" width="60">
<b style = "font-family: Arial; font-size: 16px">Note:</b><p style = "font-family:Verdana; font-size:14px">Discussion should be conducted with the process' owner</p>
</div>

## Stakeholder Analysis
<hr>
<span style ="font-family:Verdana; font-size:16px; text-align:justify">In this project we will only be mapping the stakeholders that were mentioned in articles or sources with high impacts and major role to the automatidata project.</span>

<h3 style = "text-align:center">Table 1.2. Stakeholder Analysis</h3>
<table style="color:black;
           display:fill;
           border-colapse: colapse;
           width: 100%;
           border: 1px solid black;
           border-collapse: collapse;
           border-style: solid;
           border-radius:5px;
           background-color:#5642C5;
           font-size:110%;
           font-family:Verdana;
           letter-spacing:0.5px">
  
  <tr>
    <th>Stakeholders</th>
    <th>Role</th>
    <th colspan="2">Involvement</th>    
    <th>Power or Influence (H/M/L)</th>
    <th>Interest (H/M/L)</th>
    <th colspan="2">Engagement</th>  
  </tr>
  <tr>
    <td>Jamal Harris, Director, Customer Data
</td>
    <td style = "text-align:left">      
      Project sponsor 
    </td>
    <td colspan="2" style ="text-align:left">
    Makes high-level decisions; serves as team resource
    </td>
    <td style ="text-align:center">
      H 
    </td> 
    <td style ="text-align:center">
      L
    </td>
    <td colspan="2" style ="text-align:left">
      Communicate regularly, but not daily. Ask questions and give updates. 
    </td>
  </tr>
  <tr>
    <td>Sara Romero, VP, Marketing
      and Ernest Cox, VP, Product Development</td>
    <td style = "text-align:left">      
      Project owner 
    </td>
    <td colspan="2" style ="text-align:left">
     <ul>
         <li>advisory role and providing valid information
         <li>Implementation of preventive, diagnosis and treatment measures
         <li>Allow re-export of surplus imported data or any required items to support project
         <li>Formulation of the business requirements
        <li>Formulation and implementation of equitable distribution of execution
        </ul> 
    </td>
    <td style ="text-align:center">
      M 
    </td> 
    <td style ="text-align:center">
      H 
    </td>
    <td colspan="2" style ="text-align:left">
      <ul>
        <li>Informing and public education
        <li>Monitoring the proper implementation of interventions
        <li>Coordination in informing
        <li>Official information reference in the transportation management and
control
        <li>Training and consulting with other related organizations and institutions
        </ul> 
    </td>
  </tr>
  <tr>
    <td>Wahyu Ardhitama, Head of Data Analytics</td>
    <td style = "text-align:left">      
      Project leader 
    </td>
    <td colspan="2" style ="text-align:left">
     <ul>
      <li>Project-rules making and planning
     <li>Facilitate and synergy in inter-sectorial cooperation
     <li>Identifying problems and providing solutions in the form of executive
       approvals
     </ul> 
    </td>
    <td style ="text-align:center">
      M 
    </td> 
    <td style ="text-align:center">
      H 
    </td>
    <td colspan="2" style ="text-align:left">
       <ul>
      <li>Synergy and strengthening of various capabilities across the team and organization,
       directing and Mobilizing all capacities within the team.
      <li>Lead project from the start to clossing.
      </ul> 
    </td>
  </tr>
 </table>

  <h3 style = "text-align:center">Table 1.3. Project Charter</h3>
<table style="color:black;
           display:fill;
           border-colapse: colapse;
           width: 100%;
           border: 1px solid black;
           border-collapse: collapse;
           border-style: solid;
           border-radius:5px;
           background-color:#5642C5;
           font-size:110%;
           font-family:Verdana;
           letter-spacing:0.5px">
  
  <tr>
    <th colspan ="4" style="text-align:center">Project NYC Citibike Business Plan</th>
  </tr>
    <tr>
    <th colspan ="4" style="text-align:center">2nd Aug 2023</th>
  </tr>
  <tr>
      <th colspan ="4" style="text-align:center">Document Status: <del>Draft</del> | In Review | <del>Approved</del></th>
  </tr>
  <tr>
      <th colspan ="4" style="text-align:center">Executive Summary</th>
  </tr>
  <tr>
      <td colspan ="4" style="text-align:center">develop a prediction model that predicts bike trip using location and time of day data.</td>
  </tr>
  <tr style ="background:LightSkyBlue;text-align:center">
      <td colspan ="2">Business Case</td>
      <td colspan ="2">Problem/Opportunity Statement</td>
  </tr>
 <tr style="text-align:left">
     <td colspan ="2">After the program's one-year anniversary in May 2014, membership experienced a decline from 105,355 in May to 96,318 in June. The downward trend persisted in July, leading to a total of 93,501 members. An audit conducted between May 2013 and May 2014 highlighted issues with irregular maintenance, poorly cleaned bicycles, and inadequate docking stations, all of which inconvenienced riders and hindered the system's growth. Furthermore, numerous complaints were received from customers.
<br>By October 2014, membership had further decreased to 89,286, resulting in an estimated loss of  ~\$1.53 millions (calculated based on a price of \$95 per membership). Fortunately, the executed improvement initiatives yielded positive results. Membership rebounded beyond the 2014 level, surpassing 120,000 members, which translates to an increase of over ~\$2.9 millions  (calculated at a price of \$95 per membership). With the introduction of a new price of $149, the total increase equates to \$4.5 millions. In addition, with the transition of the annual membership cost for NYHCA resident enrollment from an upfront payment of \$60 per year to a monthly fee of \$5,  it can be reasonably estimated (given the absence of specific financial data) that the initiatives have the potential to accumulate over \$2 million.</td>
      <td colspan ="2">Launched in 2013, by the end of that year, memberships had surged to 94,125, accompanied by a fleet of 6,000 bikes and 300 stations. Despite receiving numerous customer complaints about its services, Citi Bike went ahead and raised its annual membership fee from \$95 to \$149, which led to an anticipated decline in membership. Nevertheless, following a series of improvement initiatives as mentioned earlier, by September 2015, the fleet had expanded significantly, encompassing 7,454 Citi Bikes. This milestone represented a substantial advancement toward reaching the 2017 goal and the phase II expansion of Citibike. This new count constituted over 50% of the target, which aimed for 750 stations and 12,000 bikes by the conclusion of 2017. Furthermore, the count of stations had surged by 40.24% in comparison to the numbers from 2014. The team in New York City is dedicated to examining trips that are particularly susceptible to influences such as the distance between start/departure and end/destination stations, as well as the time of day. This analytical effort aims to bolster the company's strategies for enhancing performance.</td>  
  </tr>

 <tr style ="background:LightSkyBlue;text-align:center">
      <td colspan ="2">Goal Statement</td>
      <td colspan ="2">Deliverables (Key Results)</td>
 </tr>
 <tr style="text-align:left">
      <td colspan ="2">Primary metric:
     <ul>
         <li>Total trip
     </ul>
     Secondary Metric:
     <ul>
         <li>Average trip duration
         <li>Customer calls
     </ul>
     </td>
      <td colspan ="2">Primary Key Results:
     <ul>
         <li>Total number of trips
     </ul>
     Secondary Key Results:
     <ul>
         <li>Minutes
         <li>Calls per ride
     </ul>
     </td>
  </tr>
 
 <tr style ="background:LightSkyBlue;text-align:center">
      <td colspan ="2">Benefits, Cost, and Budget</td>
      <td colspan ="2">Scope and Exclusion</td>
 </tr>
 <tr style="text-align:left">
      <td colspan ="2">Benefits:
     <ul>
         <li>Increase number of trip and duration of ride
         <li>Customer satisfaction
     </ul>
     Costs:
     <ul>
         <li>Unservice/loss order
         <li>investment for new location and old location (bikes, kiosk, station, system, etc.)   
     </ul>
     Budget Needed:
           <span>TBD</span>
     </td>
      <td colspan ="2">In-Scope:
     <ul>
         <li>In area New York
         <li>Borough and neighborhood location   
         <li>2014 and 2015
     </ul>
     Out-of-Scope:
     <ul>
         <li>Revenue
         <li>Lean measure such as ,fastest processes, routes etc.
         <li>Bike types
         <li>Location characterization (commercial, residential, etc)
         <li>Supply and IT
         <li>Maintenance
         <li>Competitor
     </ul>
     </td>
  </tr>   
 
 <tr style ="background:LightSkyBlue;text-align:center">
      <td colspan ="2">Project Team</td>
      <td colspan ="2">Measuring Success</td>
 </tr>
 <tr style="text-align:left">
      <td colspan ="2"> 
     <ul>
         <li>Sponsor: Jamal Harris, Director, Customer Data
         <li>Owner: Sara Romero, VP, Marketing and Ernest Cox, VP, Product Development
         <li>Leader: Wahyu Ardhitama, Head of Data Analytics
         <li>Member: Nina Locklear, Director, Procurement, Adhira Patel, API Strategist, Megan Pirato, Data Warehousing Specialist, Rick Andersson, Manager, Data Governance, Tessa Blackwell, Data Analyst, Brianne Sand, Director, IT and Shareefah Hakimi, Project Manager
     </ul>
     </td>
  
  <td colspan ="2">Deliverables after solutions implementation:
     <ul>
         <li>Predict the neighborhood station to invest using area characterization(next)
         <li>Optimize total trip
         <li>Optimize season trip 
     </ul>
  </td>
  </tr>
  </table>

<hr>
<table style="color:black;
           display:fill;
           border-colapse: colapse;
           width: 100%;
           border: 1px solid black;
           border-collapse: collapse;
           border-style: solid;
           border-radius:5px;
           background-color:#5642C5;
           font-size:110%;
           font-family:Verdana;
           letter-spacing:0.5px">
            
  <h3 style = "text-align:center">Table 1.4. NYC Citibike Customer Top Pareto (80%) </h3>
  <tr>
    <th>Neighborhood Departure</th>
    <th>Neighborhood Destination</th>    
  </tr>
  <tr style = "text-align:center">
      <td><img style= "margin:auto" src="https://i.imgur.com/eSF4Nsc.jpg" width = "600"></td>
      <td><img style= "margin:auto" src="https://i.imgur.com/r0mnPCI.jpg" width = "600"></td>
  </tr>
  </table>



<img style="float:left" src="https://i.imgur.com/wpcEXQC.png" width="50"><div style = "font-family: Arial; font-size: 16px">
    <h1>Execute</h1></div>

<hr>
<table style="color:black;
           display:fill;
           border-colapse: colapse;
           width: 100%;
           border: 1px solid black;
           border-collapse: collapse;
           border-style: solid;
           border-radius:5px;
           background-color:#5642C5;
           font-size:110%;
           font-family:Verdana;
           letter-spacing:0.5px">
            
  <h3 style = "text-align:center">Table 2. Machine Learning Model Feature Importance </h3>
  <tr>
    <th>Logistic Regression</th>
    <th>Random Forest</th>    
    <th>XG Boost</th>
  </tr>
  <tr style = "text-align:center">
      <td><img style= "margin:auto" src="https://i.imgur.com/RzhEuBt.png" width = "600"></td>
      <td><img style= "margin:auto" src="https://i.imgur.com/3c9lod9.png" width = "600"></td>
      <td><img style= "margin:auto" src="https://i.imgur.com/QcsCIgg.png" width = "600"></td>
  </tr>
  </table>

# Conclussion
<hr>

<div class="alert alert-block alert-success" style="font-family:verdana; font-size:14px">

Logistic Regression
<br><br>
The logistic regression model achieved 100% (all weighted averages), and accuracy of 100%, on the test set which we need to be skeptical as there can be data leakage and overfitting as the data is imballance more than 85% towards the annual membership.
<br><br>
Tree-based Machine Learning
<br><br>
The result is similar to logistic regression. Here we decided to combine Random forest and XG Boost feature importance results.
<br>    
The models and the feature importances extracted from them, along with the survey results, confirm that in order to encourage the acquisition of annual memberships, it is crucial to raise awareness about the health and safety benefits of biking among the younger generation. This should be done in correlation with emphasizing the significance of trip duration and distance.
<br><br>
To acquire annual membership, the following recommendations could be presented to the stakeholders:
<li>Establish initiatives for safe cycling, including safety training and education, distribution of safety equipment, and related endeavors.
<li>Foster community partnerships and programs, such as bike ambassadors, youth and family engagement, grants for low-income individuals, etc.
<li> Expand station or location within the top departure and destination neighborhoods particularly as displayed in the feature importance results. Additionally, delve into exploring the distinct characteristics of these top locations.
<li>The growth observed in 2015 demonstrates a clear seasonality pattern, characterized by a gradual rise during the summer months, reaching its peak in September during the fall, and subsequently experiencing a gradual decline. This trend allows us to concentrate on medium to large maintenance activities during the slower seasons. These maintenance activities could include workshop repairs, strategic planning, or acquiring new assets. The execution of these maintenance efforts can be initiated after the winter period, just before the onset of the summer season when the number of riders is expected to rise. This is an opportune time to implement on-the-spot repairs as needed.   
<li>Allocate resources for repair and maintenance on-site, with a particular focus on quality checks in top trip areas during off-peak hours and particularly warm season.
<li>Hire both seasonal and permanent staff members who can actively engage with communities and contribute to the organization's objectives.
<li>Implement marketing and promotional awareness campaigns, such as #Bike4Youth and bike health events, as well as prominently displaying the NYCHA residents rate $5 per month at stations.
<br><br>
Next Steps
<br><br>
Scenario of possibilities to understand this model is required. By considering the data from the four models with the complete dataset, we observe a 100% accuracy across decision tree, random forest, and XGBoost models. Building upon the insights shared in part 2, we can further delve into the analysis of trip distances categorized as short, medium, and long distances. Regarding trip durations, we have introduced additional columns to account for overtime. In the future, we might consider incorporating another duration metric that reflects the permissible time during the day, potentially leading to the removal of the original trip duration column. Furthermore, we can consider creating columns that categorize areas based on factors such as subway access, residential nature, commercial activity, recreational facilities, Instagram-worthy spots, and tourist attractions. Also, we can distinct the bike id into e-bike and reg-bike columns. Moreover, leveraging Pareto data, we can stratify trips into quartiles: the top 25% as high trips, the middle 50% as medium trips, the subsequent 80% as low trips, and any beyond the 80% threshold as developmental trips.
<br>
As also mentioned earlier, the availability of user IDs allows us to categorize bikers into distinct groups such as platinum, frequent, high, medium, and low bikers. <b>This approach underscores the importance of user ID tracking, enabling us to determine the precise number of registered members who actively engage with the bike-sharing service. This, in turn, aids us in determining the optimal allocation of bike investments based on the observed demand patterns. Furthermore, we can conduct surveys to gain insights by sampling from the members, determining whether it is the demand or supply side that requires attention and adjustments. </b> This approach unlocks further potential for feature refinement.
<br><br>
We can also see the cluster from this model which k = 28.
</div>
