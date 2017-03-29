# Logic App Demo
## Twitter Sentiment

### Create Logic App
1.  Log into Azure
2.  Click the **Green Plus** (**New button**) on the top left of the screen
3.	Click “**Enterprise Integration >**”
4.	Select **Logic App**
5.	In the **Name** Textbox type “**LogicAppDemo**”
6.	Select the proper Subscription
7.	Create a **New Resource Group** called “**LogicAppRG**”
8.	Select the proper **Location: West US**
9.	Check the “**Pin to dashboard**” checkbox
10.	Click the **Create** button

### Add Twitter Connection
1.	Click the **Blank Logic App** tile under “Templates”
2.	Click on the **Twitter** service tile
3.	Select the **Trigger**: “**When a new tweet is posted**”
4.	**Sign in** to Twitter
5.	Add **Search Text**: *Azure*, *#UnlockMachineLearning*
6.	Adjust **Frequency** and **Interval**

### Create a Cognitive Service
1.	Open a **New Browser Tab** in Azure
2.	Click the **Green Plus** (**New button**) on the top left of the screen
3.	Click “**Intelligence + analytics >**”
4.	Select **Cognitive Services APIs**
5.	In the **Account Name Textbox** type “**LogicAppCS**”
6.	Select the proper Subscription
7.	Select **Text Analytics API** from the **API Type** dropdown
8.	Select the proper **Location**: **West US**
9.	Select **F0** from the **Pricing Tier** dropdown
10.	Under **Resource Group** select **Use Existing**
11.	From the **Resource Group** dropdown select **LogicAppRG**
12.	Click **API Setting** then **Enable** and **Save**
13.	Check the “**Pin to dashboard**” checkbox
14.	Click the **Create** button
15.	In the **Cognitive Service blade** click **Keys** 
16.	Copy **Key 1**

### Add Cognitive Service – Text Analytics: Sentiment
1.	Go to the **Logic App Browser tab**
2.	Click the **+ New Step** button
3.	Click the **Add an action** button
4.	Search for “**Sentiment**”
5.	Click on **Text Analytics Detect Sentiment**
6.	In the **Connection Name** textbox type “**TwitterKey**”
7.	**Paste** the Cognitive Service **Key** copied in the previous section
8.	Click the **Create** button
9.	In the **Text** textbox select the **Tweet text** module

### Add Cognitive Service – Text Analytics: Key phrase
1.	Click the **+ New Step** button
2.	Click the **Add an action** button
3.	Search for “**Key Phrase**”
4.	Click on **Text Analytics Key Phrase**
5.	In the **Text** textbox select the **Tweet text** module

### Add Power BI Connection
1.	Open a **New Browser Tab**
2.	Log into **Power BI**
3.	Under **Datasets** click **Streaming datasets**
4.	Click **+ Add streaming dataset** at the top right of the screen
5.	Click on the **API** tile
6.	Click the **Next** button
7.	Turn on **Historic Data Analysis**
8.	In the **Dataset Name** textbox type “**LogicAppDataset**”
9.	Add the following **Values from Stream**:

Label | Data Type
---- | ----
Text | Text
Phrase | Text
Location | Text
Created | DateTime
Followers | Number
Sentiment | Number

10.	Click the **Create** button
11.	Click the **Done** button
12.	Go to the **Logic App Browser tab**
13.	Click the **+ New Step** button
14.	Click the **Add an action** button
15.	Search for “**Power BI**”
16.	Select **Power BI: Add rows to dataset**
17.	**Sign into Power BI**
18.	Select a **Workspace**
19.	Select a **Dataset**
20.	Select a **Table**
21.	Fill in the values as follows:

Label | Module
---- | ----
Text | Tweet text
Phrase | Key phrase
Location | Location
Created | Created at
Followers | Followers count
Sentiment | Score

22.	Click **Save** in the top left of the blade
23.	Click **Run** in the top left of the blade

### Create Reports in Power BI
1.	Go to the **Power BI Browser tab**
2.	Click the **Create Reports icon** in the Streaming datasets window
3.	**Create visuals** then click **Save** in the top right of the window
4.	Name the Report
5.	**Pin Visuals** to **Dashboard** for real-time data (*Not Live Page*)





