---
layout: post
title: "How to Perform Changes on Incremental Refresh-Enabled Power BI Dataset"
date: 2024-10-02
categories: [Power BI, Data Analytics]
tags: [data analytics, Power BI]
---

In the world of data analytics, **Power BI** plays a crucial role in developing, refreshing, and managing datasets. One powerful feature that makes Power BI stand out is **incremental refresh**—enabling only the new or updated data to be refreshed while leaving the historical data unchanged. This helps manage large datasets efficiently. However, Power BI currently doesn't support downloading an incrementally refreshed dataset via the service, which can make performing changes on the dataset a challenge.

In this article, we’ll walk you through the step-by-step process of working with an incrementally refreshed Power BI dataset, making necessary changes, and overcoming the challenge of using the `.bim` file format, which is typically not readable by Power BI Desktop.

## Challenges with Incremental Refresh in Power BI

A key limitation is that Power BI does not allow you to download an incrementally refreshed dataset directly from the service. This can create roadblocks for development and changes, especially if you're managing the dataset's source control with tools like **Azure DevOps**, where the model is stored as a `.bim` file. The `.bim` format isn't natively supported by Power BI Desktop, making it difficult to view or make changes to the dataset locally.

However, by following the steps outlined below, you can extract, modify, and redeploy an incrementally refreshed dataset, working around these limitations.

## Step-by-Step Guide: How to Work on Incremental Refresh-Enabled Power BI Dataset

### Step 1: Create a Blank Power BI Project File
1. Open Power BI Desktop and create a blank report.
2. Save the report as a Power BI Project file (.pbip). If the Power BI Project file type is not available, you may need to enable this feature. To do so:
   - Navigate to **File > Options and Settings > Options**.
   - Under **Preview Features**, enable **Power BI Project (.pbip)** and restart Power BI Desktop.

   When you save the project, Power BI Desktop will create two folders alongside the .pbip file:
   - **.Dataset**: Contains your model information, including the `.bim` file.
   - **.Report**: Contains the report visuals and layout.

### Step 2: Locate the .bim File
Once the `.pbip` file is saved, open the folder where the file was saved. Inside the **.Dataset** folder, you will find the `.bim` file, which holds the model definition of your Power BI dataset.

### Step 3: Access DevOps and Navigate to the Dataset Folder
To get the latest version of the dataset:
1. Open Azure DevOps and navigate to your project repository.
2. Go to the **develop** branch and locate the **.Dataset** folder, which contains the up-to-date version of your dataset’s `.bim` file.

### Step 4: Download and Replace the .bim File
1. Download the `.bim` file from the **develop** branch in DevOps.
2. Replace the `.bim` file located in the **.Dataset** folder you created in Power BI Desktop with the one you downloaded from DevOps.

This ensures that your local Power BI Project now has the latest version of the dataset model.

### Step 5: Open and Develop Using the Power BI Project File
Now that the dataset is updated:
1. Open the `.pbip` file in Power BI Desktop.
2. Power BI Desktop will now load the dataset information, which you can modify as needed. You can also export the updated dataset to a `.pbit` (Power BI Template) file for further development and sharing.

By following these steps, you're able to download, modify, and redeploy changes to an incrementally refreshed Power BI dataset—even though it is not directly supported for download in the Power BI service.

## Key Benefits of This Approach
- **Source Control**: Using DevOps ensures that changes are version-controlled, allowing multiple developers to collaborate on the dataset efficiently.
- **Maintaining Incremental Refresh**: You can keep your dataset’s incremental refresh capabilities intact while still being able to make changes and deploy new versions.
- **Flexibility for Development**: Exporting the project as a `.pbit` template allows for further modification and testing before re-deploying the model to the Power BI service.

## Best Practices for Managing Incremental Refresh Datasets in Power BI
- **Automate Incremental Refresh Settings**: For large datasets, always configure incremental refresh to optimize data loading times and avoid refreshing historical data unnecessarily.
- **Use Power BI Dataflows**: Where possible, use Dataflows to store the intermediate stages of your data transformation, which can also be incrementally refreshed and reused across multiple reports.
- **Source Control with Azure DevOps**: Integrating Azure DevOps for source control ensures that you maintain a clear history of all changes to your datasets and models.

## Conclusion
While Power BI’s incremental refresh feature is an excellent tool for managing large datasets, it presents certain challenges when it comes to making changes to the dataset. By leveraging Power BI Projects, DevOps, and `.bim` files, you can work around these limitations and continue to develop and modify your dataset without losing the benefits of incremental refresh.

By following this guide, you can now manage, update, and redeploy changes to your Power BI dataset effectively. This method allows for ongoing development and collaboration while maintaining optimized refresh strategies for large datasets.
