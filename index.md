# CCSS OpenRefine Workshop
OpenRefine is a powerful free and open source tool for working with messy data: cleaning it and transforming it from one format into another. This lesson will teach you to use OpenRefine to effectively clean and format data and automatically track any changes that you make. Many people comment that this tool saves them literally months of work.

## Setup
For this lesson you will need the following:
- [OpenRefine](https://openrefine.org/). Detailed instructions for Windows and Mac are available: https://datacarpentry.org/openrefine-socialsci/setup.html 
  - If after installation and running OpenRefine, it does not automatically open for you, point your browser at http://127.0.0.1:3333/ or http://localhost:3333 to launch the program.
- Any web browser
- Our common dataset: https://figshare.com/ndownloader/files/30848404 The data are a simplified version of a teaching dataset from the Studying African Farm-Led Irrigation (SAFI) database.

### Documents
We will also use the following documents:
- Class [slidedeck](https://docs.google.com/presentation/d/161-fwvXzqytGS7KW-VJHlPZO9mPh5BMd9Na_8bdBy_c/edit?usp=sharing)
- Our [collaborative document](https://docs.google.com/document/d/10Z07fxI0ogmSWBLDJJjnp4O2a0bH5bc9j13ujPwHV9g/edit?usp=sharing): we will use this for our exercises and to interact with each other.

## Why use OpenRefine
OpenRefine is a powerful free and open source tool for working with messy data: cleaning it and transforming it from one format into another. With OpenRefine, you can capture all actions applied to your raw data and share them as needed (such as with a journal or granting agency). 
### Class Objectives
- Install and start a project in OpenRefine
- Navigate the OpenRefine interface
- Perfom basic tasks to clean data
- Text facets/clustering/filter
- Identify data transformation techniques and resources for more information

### Creating a project
1. Click **Create Project** and select **Get data from This Computer**.
2. Click **Choose Files** and select the **file 2021-09-SurveyData.csv** that you downloaded in the setup step. 
3. Click **Open** or double-click on the filename.
4. Click **Next>>** under the browse button to upload the data into OpenRefine.

### Faceting
Facets are one of the most useful features of OpenRefine and can help both get an overview of the data in a project as well as helping you bring more consistency to the data. A ‘Facet’ groups all the like values that appear in a column, and then allow you to filter the data by these values and edit values across many records at the same time.

We will explore the 'Text facet'.
1. Scroll over to the **village** column.
2. Click the down arrow and choose **Facet > Text facet**.
3. In the left panel, you’ll now see a box containing every unique value in the **village** column along with a number representing how many times that value occurs in the column.
4. Try sorting this facet by name and by count. Do you notice any problems with the data? What are they?
5. Hover the mouse over one of the names in the **Facet** list. You should see that you have an **edit** function available.

### Clustering
In OpenRefine, clustering means “finding groups of different values that might be alternative representations of the same thing”. For example, the two strings New York and new york are very likely to refer to the same concept and just have capitalization differences. Likewise, Gödel and Godel probably refer to the same person. 
1. In the **village** Text Facet we created in the step above, click the **Cluster** button.
2. In the resulting pop-up window, you can change the **Method** and the **Keying Function**. Try different combinations to see what different mergers of values are suggested.
3. Select the **key collision** method and **metaphone3** keying function. It should identify two clusters.
4. Click the **Merge?** box beside each cluster, then click **Merge Selected and Recluster** to apply the corrections to the dataset.

### Transforming data
The data in the items_owned column is a set of items in a list. The list is in square brackets and each item is in single quotes. Before we split the list into individual items in the next section, we first want to remove the brackets and the quotes.

Getting started:
1. Click the down arrow at the top of the **items_owned** column. Choose **Edit Cells > Transform...**
2. This will open up a window into which you can type a GREL expression. GREL stands for General Refine Expression Language.
3. We will remove all of the left square brackets. In the Expression box type **value.replace("[", "")** and click OK.
4. What the expression means is this: Take the value in each cell in the selected column and replace all of the “[” with “” (i.e. nothing - delete).
5. Click **OK**. You should see in the **items_owned** column that there are no longer any left square brackets.

Try removing the right bracket!

Now that we have cleaned out extraneous characters from our items_owned column, we can use a text facet to see which items were commonly owned or rarely owned by the interview respondents.

1. Click the down arrow at the top of the **items_owned** column. Choose **Facet > Custom text facet...**
2. In the **Expression** box, type **value.split(";")**.
3. Click **OK**.
You should now see a new text facet box in the left-hand pane.

### Filtering
There are many entries in our data table. We can filter it to work on a subset of the data in the list for the next set of operations. Please ensure you perform this step to save time during the class.

1. Click the down arrow next to **respondent_roof_type > Text filter**. A **respondent_roof_type** facet will appear on the left margin.
2. Type in **mabat** and press return. There are 58 matching rows of the original 131 rows (and these rows are selected for the subsequent steps).
3. At the top, change the view to **Show** 50 **rows**. This way you will see most of the matching rows.

### Sort
You can sort the data by a column by using the drop-down menu in that column. There you can sort by text, numbers, dates or booleans (TRUE or FALSE values). You can also specify what order to put Blanks and Errors in the sorted results.

### Undo/Redo
It’s common while exploring and cleaning a dataset to discover after you’ve made a change that you really should have done something else first. OpenRefine provides Undo and Redo operations to make this easy.

### Using Scripts
As you conduct your data cleaning and preliminary analysis, OpenRefine saves every change you make to the dataset. These changes are saved in a format known as JSON (JavaScript Object Notation). You can export this JSON script and apply it to other data files. If you had 20 files to clean, and they all had the same type of errors (e.g. misspellings, leading white spaces), and all files had the same column names, you could save the JSON script, open a new file to clean in OpenRefine, paste in the script and run it. This gives you a quick way to clean all of your related data.

### Saving/Exporting Project
By default OpenRefine is saving your project continuously. If you close OpenRefine and open it up again, you’ll see a list of your projects. You can click on any one of them to open it up again.

You can also export a project or cleaned data. A project is helpful if you wanted to send your raw data and cleaning steps to a collaborator, or share this information as a supplement to a publication.

## Additional Resources

- [Data Cleaning with OpenRefine for Social Science Data](https://datacarpentry.org/openrefine-socialsci/)
- [OpenRefine User Manual](https://docs.openrefine.org/)
- [Cleaning Data with OpenRefine (The Programming Historian)](https://programminghistorian.org/en/lessons/cleaning-data-with-openrefine)
- [Fetching and Parsing Data from the Web with OpenRefine (The Programming Historian)](https://programminghistorian.org/en/lessons/fetch-and-parse-data-with-openrefine)
- [Grateful Data](https://github.com/scottythered/gratefuldata/wiki) is a fun site with many resources devoted to OpenRefine, including a nice tutorial.

## Credits
Parts of this workshop are adapted from [The Carpentries' "OpenRefine for Social Science Data" workshop](https://datacarpentry.org/openrefine-socialsci/). Licensed under [CC-BY 4.0](https://creativecommons.org/licenses/by/4.0/).
