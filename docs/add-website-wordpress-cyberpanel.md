---
title: Add Website & WordPress in CyberPanel
sidebar_label: Add Website & WordPress in CyberPanel
sidebar_position: 5
---

## Adding a New Website in CyberPanel

This guide will walk you through the steps to add a new website in CyberPanel, a powerful control panel for managing your server and websites.

### Step 1: Access CyberPanel
- Open your web browser and go to `https://<your-server-ip>:8090`.
- Log in with your admin username and password.

### Step 2: Navigate to Websites
- Once logged in, go to the **Websites** section in the left sidebar.
- Click on **Create Website**.

### Step 3: Fill in Website Details
- **Select Package**: Default
- **Select Owner**: Choose the owner of the website (admin).
- **Domain Name**: Enter the domain name for the new website (example.com).
- **Email**: Enter the email address associated with the website.
- **PHP Version**: Select the PHP version you want to use (8.1 -> it's more stable with themes and plugins).
- Make sure "Create Mail Domain" is uncheck.

### Step 4: Create the Website
- After filling in all the details, click on **Create Website**.
- CyberPanel will process the request and set up the new website.

### Step 5: Verify Website Creation and Install wordpress
- Once the website is created, you will see it listed under the **List Websites** section.
- Click on the domain name of the newly created website to access its management page.
- To install WordPress, navigate to the **Application Installer** section.
- Select **WordPress** from the list of available applications.
- Fill in the required details for the WordPress installation:
  - **Site Title**: Enter the title for your WordPress site.
  - **Admin Username**: Choose a username for the WordPress admin.
  - **Admin Password**: Set a strong password for the admin account.
  - **Admin Email**: Enter the email address for the admin account.
- Click on **Install Now** to begin the WordPress installation.
- Once the installation is complete, you can access your WordPress site by visiting `http://<your-domain>/wp-admin` and logging in with the admin credentials you set.

### Step 6: Change PHP Version to 8.1
- After installing WordPress, the PHP version might be set to 8.0 by default.
- To change it to 8.1, go to the **Websites** section in CyberPanel.
- Click on **List Websites** and select the domain you want to modify.
- In the management page, find the **PHP** section.
- Select **Change PHP** and choose version 8.1 from the dropdown menu.
- Click **Save Changes** to apply the new PHP version.