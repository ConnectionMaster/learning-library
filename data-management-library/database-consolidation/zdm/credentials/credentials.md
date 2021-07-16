# Creating the Target Autonomous Database Credential

## Introduction
In this lab, you will be:
  * Creating an authentication token for your Oracle Cloud Infrastructure (OCI) user profile.
  * Logging into your migration target autonomous database and creating the credential file you will need to connect to your OCI user.
  * Creating movedata\_user in the autonomous database.

Estimate Lab Time: 15 minutes

## **STEP 1: Create Authentication Token**
1. Go to your OCI profile by selecting the icon in the top right and clicking user.
    ![Dashboard Profile](./images/dashboard-profile.PNG)

2. Under Resources in the bottom left select Auth Tokens and click generate token.
    ![Authentication Token](./images/auth-token.PNG)

3. Set a description and click generate token and make sure to write down the token displayed as you cannot get access to it again. If you lose the token you will need to generate a new one.
    ![Token Description](./images/token-desc.PNG)

## **STEP 2: Log Into SQL on the Autonomous Database**
1. In your OCI Dashboard: select the hamburger menu, Oracle Database. Autonomous Database.
    ![Autonomous Menu](./images/menu-auton.PNG)

2. Select the target database.
    ![Select Autonomous](./images/select-auton.PNG)

3. In the database menu go to Tools -> Open Database Actions.
    ![Database Action](./images/db-action.PNG)

4. Fill in ADMIN for the username and the password will be `WELcome123ZZ` unless you set it as something different.

5. Select SQL
    ![Select SQL](./images/select-sql.PNG)


## **STEP 3: Run Credential Script**
1. In the script below replace `<oci_user>`, `<oci_tenancy>`, `<api_private_key>`, and `<fingerprint>` with their respective information and paste it into SQL.
  * `<oci_user>`, `<oci_tenancy>`, and `<fingerprint>` are in the Configuration File Preview under API Keys in your OCI user profile from the previous labs.
  * `<api_private_key>` is your API private key from the Host Environment lab. To view it again, in command prompt as 'zdmuser':

    ```
    <copy>
    cd ~
    cd .oci
    cat oci_api_key.pem
    </copy>
    ```

    SQL Script

    ```
    <copy>
    begin
    DBMS_CLOUD.CREATE_CREDENTIAL (
    'DEF_CRED_NAME',
    '<oci_user>',
    '<oci_tenancy>',
    '<api_private_key>',
    '<fingerprint>');
    end;
    /
    </copy>
    ```

2. Select 'Run Script'.
    ![Credential Script](./images/cred-script.PNG)

## **STEP 4: Create User in Autonomous**
1. You will need to pre-create movedata\_user in the autonomous database.

2. Test to make sure the user doesn't already exist by running the drop command. It is fine if it fails:

    ```
    <copy>
    drop user movedata_user cascade;
    </copy>
    ```

3. Create the user and grant it privileges:

    ```
    <copy>
    create user movedata_user identified by WELcome123ZZ;
    grant dwrole to movedata_user;
    </copy>
    ```



## Acknowledgements
* **Author** - Zachary Talke, Solutions Engineer, NA Tech Solution Engineering
* **Last Updated By/Date** - Zachary Talke, July 2021
