# Getting Started with Data Visualization: Using Tableau and Google Dataset Search

As a first task to get our feet wet with **data visualization,** we're instructed to find a **free dataset** that is publicly available using [Google Dataset Search.](https://datasetsearch.research.google.com/)

With our dataset, we will be using a very prominent data visualization software: **Tableau.** Tableau is used by professional data analysts and newbies alike. You might often hear Tableau described as "the next generation of Excel." That is, Tableau can be used to quickly and easily analyze data while also offering more advanced data customization features. [**Tableau Public** is free to download,](https://public.tableau.com/app/discover) so that is the iteration of the software we will be working with today.

For this task, we will be creating a **geographic map** using the data we find. Therefore, it is very important that we choose a dataset that has a built-in "Addresses" column or geographic coordinate information. This helps Tableau automatically associate our data with a map. Later on when we complete more advanced tasks with Tableau, it will be possible to add a spatial dimension to other datasets which lack one. But for now, we're going to stick to a simple exercise to demonstrate Tableau's capabilities.

## To begin, I've selected a dataset of Florida's Recreation Facilities and Parks.
[This data](https://hub.arcgis.com/datasets/FDACS::florida-recreation-and-parks/explore?location=-0.000000%2C0.000000%2C0.70) was last provided as of July, 2020, courtesy of the Florida Department of Agriculture and Consumer Services. The dataset already maps nicely onto the provided visualization, but we're going to recreate it while making a few minor changes to it.

*(Note: This exercise was completed on Windows, so the guide is written for Windows users.)*

## Here's a few steps to follow to get us started:
1. Find and save your choice of dataset. *(Remember that it must include either Addresses or coordinates.)*
2. Download Tableau Public [here.](https://public.tableau.com/app/discover)
3. Open Tableau Public. *(On Windows, either launch from the Desktop shortcut or search "Tableau" using ⊞ Windows search.)*
4. From the landing screen, either click "File → New" or select the storage location of your dataset by picking either a file type or a server location (such as Google Drive) under the "Connect" heading on the left of the screen. (Either way gets you to the same place.)
5. (If you selected "File → New", then click "Data → New Data Source" from the top ribbon. Select your data from where you stored it.)
6. Similar to Excel, your dataset will open in a new sheet titled "Sheet 1", which you can find at the bottom of the window next to "Data Source".
7. Click the tab labeled "Sheet 1". On the left side of the window, under the box labeled "Data", look for the titled names of your data's columns under "Tables." These will be displayed here vertically.
8. In my data (and likely in yours), there is a column entitled "Address" which shows up under "Tables". *(Yours should be called something similar.)* Click the drop-down arrow on the right side of where that row is selected. Doing so reveals a menu that is labeled "Add To Sheet, Duplicate, Rename," ...etc.
9. To ensure that Tableau definitely recognizes the data in this column as being geographical/spatial, hover over the option labeled "Geographic Role" and select the relavent attribute type. (For example, "Address", if it appears.) In my case, "Address" was not an option and Tableau considered the data in this column "text" by default. Therefore, I opted to have Tableau create a geographic association for this data by selecting: "Geographic Role → Create from → Zipcode". This worked because there are zipcodes stored in my dataset.
10. Now, with Tableau recognizing this data as geographic, still in Sheet 1, I grabbed onto the "Address" field under "Tables" on the left side of the screen, and dragged "Address" to the blank workspace in the center of the screen where there are several boxes which say "Drop field here". (In other words, take your geographic data field and drag it into the blank workspace in the center of the screen.)
11. Tableau should generate a map automatically with your data points already on it. Now, you can begin customizing the way this map appears.
12. On the left side of the map area, there is a box of options labeled "Marks." To start, click "Color" and select the default color swatch of your choosing. This changes the color of the data points (dots) on your map. In my case, I chose green dots.
13. Next, to make the shape of the underlying map itself more visually distinguishable, you can select from a few default map views which act similar to "themes." To do so, on the ribbon at the top of the screen, select "Map → Background Maps". You can click through each of these to change the visual appearance of your map and decide which works best. In this case, I chose "Normal".
14. You could continue playing around with Tableau making other changes if you want, but at this point, you're done!
15. To export your map as an image, in Tableau Public, you need to publish your map using "File → Save to Tableau Public". *(In some cases, you may be able to use "Worksheet → Export", but if this doesn't work, then follow the remaining instructions.)*
16. Once you have signed into your Tableau Public account and the map has been successfully published, a webpage window will open where you can view it. From the webpage, where the map appears, there is a toolbar at the bottom where it says "View on Tableau Public".
17. From this webpage, select the download icon (the rectangle with the down-facing arrow) and click "Image". The image file of your map will be downloaded to wherever you store your Downloads by default on your computer (such as in "Downloads").

## And here is the result:
![Florida Recreation and Parks](https://github.com/user-attachments/assets/14f2f56a-d5a4-40f5-97bd-7a6f29295f0e)



