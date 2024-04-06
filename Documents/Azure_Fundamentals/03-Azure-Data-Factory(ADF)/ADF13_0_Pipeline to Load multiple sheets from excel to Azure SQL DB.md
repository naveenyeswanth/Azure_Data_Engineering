# Load multiple sheets from excel to Azure SQL DB
**Step 1: Create Excel with sample data**
  - Open excel > in Sheet1 type as shown below

    ![image](https://user-images.githubusercontent.com/20516321/191252721-c4e945f6-6823-4747-a86f-e5ab65cf334f.png)

  - In Sheet2 type as shown below

    ![image](https://user-images.githubusercontent.com/20516321/191252829-46b4751e-0949-491b-95bd-bc476b85b506.png)

  - save it > name it as **Load_multiple_sheets_of_excel**
  
**Step 2: Upload Excel into Blob container folder**
  - Open > portal.azure.com > go to **storage account** > open **container** > open **folder** > upload above excel

**Step 3: Create source dataset wth sheetname as parameter**
  - Open **ADF Studio** > Click on **Author** > expand **Datasets** > Navigate to required folder > click on folder **...** > click on **New DataSet**
  - Select **Azure Blob Storage** > Click on **Continue** > Select **Excel** > Click on **Continue** > Name it as **src_multiple_sheets** > Select required **Linked Service** > Browse and point to above **Blob Excel** > select **First row as Header** > select import schema as **None** > Click on **ok**
  - Click on **Parameters** > Click on **New** > provide as shown below

    ![image](https://user-images.githubusercontent.com/20516321/191262796-d7b25243-8387-4eba-94ff-526498ded16e.png)
    


  - Clcik on **Connections** > Click on  **SheetName** > Click on **add dynamic content** > under **parameters** > click on **psheetname** parameter > Click on **ok**
  


    ![image](https://user-images.githubusercontent.com/20516321/191746516-27235344-7af2-41c1-9342-13a97f365f27.png)
    

**Step 4: Create Target dataset**
  - Open **ADF Studio** > Click on **Author** > expand **Datasets** > Navigate to required folder > click on folder **...** > click on **New DataSet**
  - Select **Azure SQL Database** > Click on **Continue** > Name it as **tgt_multiple_sheets** > select required **Linked Service** > Click on **Edit** > provide required schemaname and table name > select **none**
  - Click on **ok**

    ![image](https://user-images.githubusercontent.com/20516321/191257544-6f49fafb-1a42-4a71-92b7-8b1809a462ad.png)


**Step 5: Create Pipeline**

  - Open **ADF Studio** > Click on **Author** > expand **Pipelines** > Navigate to required folder > click on folder **...** > click on **New Pipeline**
  - Name pipeline as **p05_pipeline_load_multiple_sheets_to_azure_sql_database**
  - Click on **Variables** > Click on **New** > Provide as shown below
    
    ![image](https://user-images.githubusercontent.com/20516321/191259230-ae9fe749-6cde-40c2-abdd-11b4f0ca2a89.png)

  - From **Activities** > expand **Itteration & Conditionals** > drag and drop ** **ForEach** into work area
  - Click on **Settings** > select **Sequential** > Click on **Items** > click on **add dynamic content** > Click on **Variables** > click on **list_of_sheets** > clcik on **ok**

    ![image](https://user-images.githubusercontent.com/20516321/191260526-110579a8-5832-4aba-b0db-df82bd48759f.png)

  - Click on **Activities** > Click on **Edit** > drag and drop **CopyData** > Clcik on **Source** > Select **Source Dataset** > select **src_multiple_sheets** > Under **Dataset Properties** > Click on parameter **pSheetName** > Click on **add dynamic content** > Under **ForEachItterator** > click on **ForEach1** > Click on ok
  - Click on **Additional coumns** >> New >> provide as shown below
![image](https://user-images.githubusercontent.com/20516321/192457692-864308ab-32f6-4f57-b19c-79751df6ea6c.png)

  - Click on **Sink** > Select Sink Dataset as **tgt_multiple_Sheets** > Select **table option** as **Auto Create** > Click on **publish all** 

**Step 6: Trigger Pipeline**
  - Click on **Add Trigger** > Click on **Trigger now**
  - observe run status

     ![image](https://user-images.githubusercontent.com/20516321/209803014-312e7b9c-2c8e-4aca-af0b-d54870d76cda.png)


  - go to database and query target table andobserve both records

    ![image](https://user-images.githubusercontent.com/20516321/209803533-21b87745-5ccf-401e-831f-deeb7f17b036.png)

# Questions
1. dataset level what all are can be parameterized?
  - We can parameterize al possible options like
       - 1. container name
         2. foldername
         3. file name
         4. sheet name
         5. schema name
         6. tablename
2. In this chapter did you learned Pipeline level array variable?
  - True

## Related Content: 

1. [get dynamically all sheets using index numbers](https://learn.microsoft.com/en-us/answers/questions/986785/how-to-get-excel-sheet-names-dyanamically-in-azure)
2. [ADF xlsx file Dynamic sheet name](https://learn.microsoft.com/en-us/answers/questions/767239/adf-xlsx-file-dynamic-sheet-name)


