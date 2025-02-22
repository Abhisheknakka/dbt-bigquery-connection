# Connect BigQuery with DBT via Google Cloud

This README provides step-by-step instructions to connect **BigQuery** with **DBT** using your **Google Cloud** account. No need to install the Google Cloud SDK — we'll use the cloud-based approach.

## Prerequisites

Ensure the following:

1. **Google Cloud Project** with **BigQuery** enabled.
2. **DBT Cloud Account**: You can sign up at [DBT Cloud](https://cloud.getdbt.com/).
3. **Service Account** with BigQuery permissions.

## Step 1: Create and Configure a Service Account in Google Cloud

### 1. **Create a Service Account**:
   - Go to [Google Cloud Console](https://console.cloud.google.com/).
   - Navigate to **IAM & Admin** > **Service Accounts**.
   - Click on **Create Service Account**.
   - Assign the following roles to the service account:
     - **BigQuery Data Viewer**
     - **BigQuery Job User**
     - **BigQuery User**

### 2. **Download the Service Account Key**:
   - After creating the service account, download the **JSON key** file.

### 3. **Upload the Service Account Key to DBT Cloud**:
   - Log into [DBT Cloud](https://cloud.getdbt.com/).
   - Navigate to the **Account Settings** > **Connections**.
   - Choose **BigQuery** and select **Service Account Key** as the authentication method.
   - Upload the **JSON key** file you downloaded from Google Cloud.

## Step 2: Configure DBT in DBT Cloud

### 1. **Create a New DBT Project**:
   - Once logged into **DBT Cloud**, create a new project by clicking **Create New Project**.
   - Choose **BigQuery** as the database.
   
### 2. **Set Up the BigQuery Connection**:
   - In the DBT Cloud project setup, enter the following details:
     - **Project ID**: Your Google Cloud project ID (found in Google Cloud Console).
     - **Dataset**: The dataset in BigQuery you will use.
     - **Key File**: Upload the **service account JSON key**.
   
   Example configuration:
   - **Project ID**: `your-gcp-project-id`
   - **Dataset**: `your_dataset_name`
   - **Key File**: `path/to/your/service-account-file.json`

### 3. **Test the Connection**:
   - After configuring the connection, click **Test Connection** to ensure everything is set up correctly.
   - If successful, you should see a message confirming that DBT has connected to BigQuery.

## Step 3: Create and Run a DBT Model

### 1. **Create a DBT Model**:
   - In the **DBT Cloud** interface, go to the **Models** tab and click **+ New Model**.
   - Add a SQL query to the new model file, for example:

   ```sql
   -- models/my_first_model.sql
   SELECT
     name,
     COUNT(*) AS order_count
   FROM
     `your-gcp-project-id.your_dataset_name.your_table`
   GROUP BY
     name
