# Visualizing a Social Network Using NodeXL

This week, I experimented with creating a social network visualization utilizing the **NodeXL plugin.** Given that I've spent a lot of time with `R` lately, I decided to stop in for a visit with Excel and try out something different.

To create the visualization, I made my own Addams Family dataset from scratch. The dataset itself consists of three columns: Person1, Person2, and Relationship, including 21 rows or "observations" of these relationships.

## Using NodeXL Basic
After downloading the NodeXL Basic plugin, I searched up the included **template** file and added in my dataset. There are two primary tabs of interest in the template: Edges and Vertices. The values input here use formulas to map data onto the visualization.

On the **"Edges" tab,** I input the values for Person1 under **Vertex 1,** and the values for Person2 under **Vertex 2.** Then, I added my custom relationship labels to the "Labels" column for each pair (ex: married, siblings, cousins, etc.) Here, I also took the liberty to change the text colors for the labels and adapted the label opacity values.

Next, I moved to the **"Vertices" tab** and input the name for each Person1 under the **Vertex** column. Importantly, these should be in identical positions on this tab as they are on the Edges tab. (For example, "Gomez Adams" should appear in A3 on both tabs.)

After handling Person1, I input the values for Person2 under the **Labels** column, still on the Vertices tab. Again, these should correspond to identical values from the "Edges" tab. Doing this tells NodeXL where to map and label values in the resulting visualization.

From here I added a few more customizations for *(attempted)* readability improvements. I set all cells in the "Size" column to size 3.0, which increased the dot size for each data point slightly. Then I ensured every cell in the "Visibility" column was set to "Show" so that they would appear on the visualization.


