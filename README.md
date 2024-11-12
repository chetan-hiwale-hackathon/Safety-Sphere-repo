## Safety-Sphere
This project for the Microsoft Fabric and AI Learning Hackathon. 


**Introduction to the Safety sphere:**

Safety Sphere is a cloud-native safety solution developed in Microsoft Fabric. It integrates data from mobile apps and smart watches for continuous monitoring and analytics. The system features geofencing alerts that use geospatial data to define safe and unsafe zones, triggering notifications if a family member exits or enters these areas.
The solution centralizes streaming data, processes real-time events, and sets up automated alerts through the Data Activator. This architecture ensures detailed visualization, enabling users to quickly detect potential safety threats and respond promptly, ensuring comprehensive protection for family members.

**Our Inspiration** :

We were inspired by the **stories and reports often heard on social media**. One of the incidents involved a person walking home from work, feeling uneasy as he noticed the streets becoming increasingly deserted. The **stories of harassment and violence against women and children** that we had read about and heard from friends echoed in your mind. This incident made me realize the importance of staying in touch and ensuring your safety, inspiring me to take proactive steps to improve our family’s communication and safety measures.

## Challenges we ran into:
One of the major challenges we faced was writing **efficient KQL queries** was also challenging, as our initial queries resulted in performance bottlenecks. Additionally, building real-time dashboards in Microsoft Fabric required careful design to handle live updates smoothly. **Creating alerts** based on the real-time dashboard data was also quite challenging.


**Architecture overview:**

![image](https://github.com/user-attachments/assets/8b525841-270b-4ae6-b66b-585547e17579)

 
1.	Data source: Real-time data is from smart phones, containing both location and health-related information in JSON format. 
2.	Data Streaming: Data in Json format is being stream to Event Hub in Event Stream with destinations KQL DB, Lakehouse and data activator. 
3.	Data Archiving and Storage:  Within the event streamer, data is archived in a Lakehouse for archival purposes. Concurrently, data is stored in a KQL database for further transformations. 
4.	Dashboard: The data is visualized from all the layers to provide comprehensive information about the user and his/her health activity like user live location, blood pressure, heartbeat, live location tracking in panic state, etc. 
5.	Monitoring and alerts: Based on the user’s real time activity, appropriate alerts have been setup using Data activator. 


**Zones and State**

1. Safe zone : This zone is added by user, where user feels safe. Ex : Home, office, etc.
2. Unsafe zone : This zone is identified by multiple panic state activated from multiple users. This multiple point is identified as cluster , thus refering to unsafe zone.
3. Panic state : A state where user feels uncomforable or feel unsafe in a area, the user must activate panic mode to get help quickly from emergency contacts which is alerted via SOS message and live location sharing. 

**Alerts**
1. SOS Messages
2. Safe zone enter / exits
3. Unsafe zone enter / exits

**Steps to setup the workspace**

**1. Create Microsoft Fabric Workspace:**
![image](https://github.com/user-attachments/assets/68878550-1343-4b2a-b24b-89f4ab5ce223)
 

**2. Create Event House** : 
- After creating Event House, a default KQL Database will be created. Rename the KQL database to a suitable name.
- Similarly, we can create Lakehouse and Data activator.

 ![image](https://github.com/user-attachments/assets/11c32ede-8af6-4084-975a-68460a82e16c)


**3. Setup the event stream:**
- Create a event stream and set source as custom endpoint and copy the EventHub name and connection string details. 
- After setting the source, select Lakehouse as destination from “Add destination” tab and fill the required parameters. Similarly add for KQL DB and Data activator.
![image](https://github.com/user-attachments/assets/f998946c-a010-472b-8df0-aeb27912b926)

 
**4. Create a notebook:**
- To simulate data ingestion from user, create notebook to write a script for data ingestion. 
- Insert data streamer notebook code and change the event-hub name and event hub connection string and run all the cells to start streaming data to eventstream. 
- Upload the dataset.parquet inside the lakehouse.
- This will stream data to event hub in event stream. Event stream will ensure to stream the data in Lakehouse, KQL database and Reflex.  
 ![image](https://github.com/user-attachments/assets/8dfc2218-bc57-475e-86a9-b426724ddb08)



**5. Setup the update policy** 
- Create a Query set and insert the update policy and tables queries and run them.
 ![image](https://github.com/user-attachments/assets/d045bbe7-0daf-4a7f-b917-0b023190e878)


**6. Create Real time dashboard:**
- Create Real time dashboard. Go to manage section and click on replace the file with dashboard.json file. 
 ![image](https://github.com/user-attachments/assets/d46d2837-95f5-42a9-a72e-58f468a4f308)

- After replacing the file, the dashboard should look like this.
![image](https://github.com/user-attachments/assets/0e10e932-90b4-4e3d-b519-05194933359b)

 
**7. Create Alerts** 
- In the data activator attached to the stream, you can the health alerts as well as the other alerts required. 
- Also we can set the alerts on realtime dashboard as required by navigating on the visual and selecting “Set alert” option. By setting up the conditions we can set up the alerts.


Contact :
If there are any questions, please do reach out to us.
1. Chetan Hiwale : chetan.hiwale@ltimindtree.com
2. Sakshi Khojare : sakshi.khojare@ltimindtree.com
3. Rutuja Chinchghare : rutuja.chinchghare@ltimindtree.com
