# Logic App Demo
## Twitter Sentiment

### Create Logic App
1.  Log into Azure
2.  Click the **Green Plus** (**New button**) on the top left of the screen

![New Button](https://github.com/nwcadence/hol-azure-logicapp/blob/master/Twitter%20Sentiment/Images/1-2%20Click%20the%20Green%20Plus%20(New%20button)%20on%20the%20top%20left%20of%20the%20screen.png?raw=true)

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

![Twitter Tile](https://github.com/nwcadence/hol-azure-logicapp/blob/master/Twitter%20Sentiment/Images/2-2%20Click%20on%20the%20Twitter%20service%20tile.png?raw=true)

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

![Key](https://github.com/nwcadence/hol-azure-logicapp/blob/master/Twitter%20Sentiment/Images/3-15%20In%20the%20Cognitive%20Service%20blade%20click%20Keys.png?raw=true)

16.	Copy **Key 1**

### Add Cognitive Service – Text Analytics: Sentiment
1.	Go to the **Logic App Browser tab**
2.	Click the **+ New Step** button
3.	Click the **Add an action** button
4.	Search for “**Sentiment**”
5.	Click on **Text Analytics Detect Sentiment**

![Text Analytics Sentiment](https://github.com/nwcadence/hol-azure-logicapp/blob/master/Twitter%20Sentiment/Images/4-5%20Click%20on%20Text%20Analytics%20Detect%20Sentiment.png?raw=true)

6.	In the **Connection Name** textbox type “**TwitterKey**”
7.	**Paste** the Cognitive Service **Key** copied in the previous section
8.	Click the **Create** button
9.	In the **Text** textbox select the **Tweet text** module

### Add Cognitive Service – Text Analytics: Key phrase
1.	Click the **+ New Step** button
2.	Click the **Add an action** button
3.	Search for “**Key Phrase**”
4.	Click on **Text Analytics Key Phrase**

![Text Analytics Key Phrase](https://github.com/nwcadence/hol-azure-logicapp/blob/master/Twitter%20Sentiment/Images/5-4%20Click%20on%20Text%20Analytics%20Key%20Phrase.png?raw=true)

5.	In the **Text** textbox select the **Tweet text** module

### Add Power BI Connection
1.	Open a **New Browser Tab**
2.	Log into **Power BI**
3.	Under **Datasets** click **Streaming datasets**
4.	Click **+ Add streaming dataset** at the top right of the screen


![Power BI Add Streaming Dataset](https://github.com/nwcadence/hol-azure-logicapp/blob/master/Twitter%20Sentiment/Images/6-4%20Click%20+%20Add%20streaming%20dataset%20at%20the%20top%20right%20of%20the%20screen.png?raw=true)

5.	Click on the **API** tile

![API Tile](https://github.com/nwcadence/hol-azure-logicapp/blob/master/Twitter%20Sentiment/Images/6-5%20Click%20on%20the%20API%20tile.png?raw=true)

6.	Click the **Next** button
7.	Turn on **Historic Data Analysis**

![Historic Data Analysis](https://github.com/nwcadence/hol-azure-logicapp/blob/master/Twitter%20Sentiment/Images/6-7%20Turn%20on%20Historic%20Data%20Analysis.png?raw=true)

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

![Power BI Add Rows](https://github.com/nwcadence/hol-azure-logicapp/blob/master/Twitter%20Sentiment/Images/6-16%20Select%20Power%20BI%20Add%20rows%20to%20dataset.png?raw=true)

17.	**Sign into Power BI**
18.	Select the **Workspace** you created the Streaming Dataset in
19.	Select “**LogicAppDataset**” from the **Dataset** dropdown
20.	Select “**RealTimeData**” from the **Table** dropdown
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

![Create Reports](https://github.com/nwcadence/hol-azure-logicapp/blob/master/Twitter%20Sentiment/Images/7-2%20Click%20the%20Create%20Reports%20icon%20in%20the%20Streaming%20datasets%20window.png?raw=true)

3.	Click the **Line Chart** icon in the **Visualizations** blade

![Line Chart](https://github.com/nwcadence/hol-azure-logicapp/blob/master/Twitter%20Sentiment/Images/3%20Line%20Chart.png?raw=true)

4.	Drag the **Created** module from the **Fields** blade to the **Axis** box in the **Visualizations** blade
5.	Drag the **Sentiment** module from the **Fields** blade to the **Values** box in the **Visualizations** blade

![Populate Fields](https://github.com/nwcadence/hol-azure-logicapp/blob/master/Twitter%20Sentiment/Images/5%20Populate%20Fields.png?raw=true)

6.	Click the **downward arrow** on the **Sentiment** module in the **Values** box 
7.	Choose **Average** to show the average sentiment over time

![Average Sentiment](https://github.com/nwcadence/hol-azure-logicapp/blob/master/Twitter%20Sentiment/Images/7%20Average.png?raw=true)

8.	Click **Save** at the top right of the window

![Save Report](https://github.com/nwcadence/hol-azure-logicapp/blob/master/Twitter%20Sentiment/Images/7-3%20Create%20visuals%20then%20click%20Save%20in%20the%20top%20right%20of%20the%20window.png?raw=true)

9.	Name the Report “**Twitter Sentiment Report**”
10.	Click the **Pin Visual** icon at the top right of the visual

![Pin Visual](https://github.com/nwcadence/hol-azure-logicapp/blob/master/Twitter%20Sentiment/Images/10%20Pin%20Visual.png?raw=true)

11.	Choose **New dashboard** then name it “**Twitter Sentiment Dashboard**”
12.	Click the yellow **Pin** button
13.	View your streaming data by selecting **Twitter Sentiment Dashboard** under **Dashboards**

## Don't forget to delete your resource group after completing the lab. This will ensure you are not unexpectedly charged for resources you are not using. 
