# DEMO - AWS Organizations

## <h2>Overview</h2>
In this demo, we will set up an AWS Organization using the <strong>GENERAL</strong> account as the MANAGEMENT account and the <strong>PRODUCTION</strong> account as a MEMBER account. We will configure cross-account access using an IAM role and demonstrate how to switch between accounts.

## <h2>Pre-Requisites</h2>

### <h3>1. AWS Account Setup</h3>
1. **Create AWS Accounts:**
   - Created two AWS accounts : <strong>farah-training-aws-general</strong> and <strong>farah-training-aws-production</strong>, we will refer to them as <strong>GENERAL</strong> and <strong>PRODUCTION</strong>.
   - These accounts will be used for all future demos.

2. **Configure Billing and Security:**
   - Set up <strong>Billing Alerts</strong> to monitor and control expenses. 
   - Enabled <strong>Multi-Factor Authentication (MFA)</strong> on the root accounts for both GENERAL and PRODUCTION.

3. **Create IAM Admin Users:**
   - Using the <strong>IAM</strong> service, created an `iamadmin` user for each account.
   - Assigned `AdministratorAccess` permissions to each `iamadmin` user.
   - Enabled <strong>Multi-Factor Authentication (MFA)</strong> on for each `iamadmin` user.
   - <strong>Access Keys</strong> were generated for each `iamadmin` user.

## <h2>Steps</h2>

### <h3>1. Set Up the Management Account</h3>
1. Open AWS Organizations in the GENERAL account.
2. Click on <strong>"Create an Organization"</strong>.
   <br/>
   
![Screenshot](https://imgur.com/xjzt5eJ.png)

### <h3>2. Invite the PRODUCTION Account using the Management Account</h3>
1. Log in to the <strong>Production</strong> account as iamadmin.
2. Copy the Production Account ID.
 <br/>
 
   ![Screenshot](https://imgur.com/m0XXGVK.png)
3. Go back to the GENERAL account, click <strong>"Add an AWS account"</strong> > <strong>"Invite Existing Account"</strong>.
4. Paste the Production Account ID, add a message if needed, and click <strong>"Send Invitation"</strong>.
<br/>

![Screenshot](https://imgur.com/DqS5zyH.png)

5. In the Production account, navigate to <strong>AWS Organizations</strong> > <strong>Invitations</strong> > <strong>Accept Invitation</strong>.
   <br/>
   
![Screenshot](https://imgur.com/Pcp2Rzf.png)

### <h3>3. Create a Role for Cross-Account Access</h3>
1. In the Production account, go to <strong>IAM</strong> > <strong>Roles</strong> > <strong>Create Role</strong>.
2. Choose <strong>AWS Account</strong> as the trusted entity.
3. Select <strong>Another AWS Account</strong> and enter the GENERAL/Management Account ID.
   <br/>
   
   ![Screenshot](https://imgur.com/hagtGVh.png)
   
4. Assign the <strong>AdministratorAccess</strong> permission.
   <br/>
   
   ![Screenshot](https://imgur.com/wkj3eP4.png)
5. Name the role `OrganizationAccountAccessRole` and click <strong>Next</strong>.

6. Navigate to <strong>IAM</strong> > <strong>Roles</strong> > `OrganizationAccountAccessRole` > <strong>Trust Relationships</strong>. The GENERAL/Management Account ID should be listed as a trusted entity.
   <br/>
   
![Screenshot](https://imgur.com/WYZgRFh.png)

### <h3>4. Switch Roles from GENERAL to PRODUCTION Account</h3>
1. Copy the Production Account ID.
2. In the GENERAL account, click on the main dropdown and select <strong>"Switch Role"</strong>.
3. Enter the Production Account ID and the role name `OrganizationAccountAccessRole`.
4. Set a display name (e.g., "PROD") and a color (e.g., Red).
5. Click <strong>Create</strong> / <strong>Switch Role</strong>.
<br/>
![Screenshot](https://imgur.com/4u4Xv7h.png)

6. We will now see the display name "PROD" in the top right menu. We can switch back to the GENERAL account as needed.
<br/>
![Screenshot](https://imgur.com/UYH7v4W.png)

### <h3>5. Create a New Account in the Organization</h3>
1. In the GENERAL account, go to <strong>AWS Organizations</strong> > <strong>Add Account</strong> > <strong>Create an AWS Account</strong>.
2. Name the new account and create it.
3. Once the new account is created, copy its account ID.
<br/>

![Screenshot](https://imgur.com/8DRzMRE.png)

4. Switch to the new account by going to the main dropdown > <strong>Switch Role</strong> > enter the new account ID > use the same role name `OrganizationAccountAccessRole` > click <strong>Switch Role</strong>.
<br/>

![Screenshot](https://imgur.com/alYixAi.png)

## <h2>Conclusion</h2>
We have successfully set up an AWS Organization with multiple member accounts. The **GENERAL** account became the **MASTER** account for the organization. We invited the **PRODUCTION** account as a **MEMBER** account and created the **DEVELOPMENT** account as an additional **MEMBER** account.
And to enable secure cross-account management, we created an `OrganizationAccountAccessRole` in the **PRODUCTION** account. This role allowed us to seamlessly switch between accounts and manage resources across the organization.



