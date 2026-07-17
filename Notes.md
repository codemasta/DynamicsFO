![d365 overview](Images/d365overview.png)

It's offered in the Cloud by Microsoft. So each organization is considered as a tenant.

![d365 tenant](Images/tenants.png)

https://learn.microsoft.com/en-us/credentials/certifications/d365-functional-consultant-financials/?practice-assessment-type=certification


LAB for online trials : https://learn.microsoft.com/en-us/training/modules/get-started-financial-management-dyn365-finance/12-1-exercise?ns-enrollment-type=learningpath&ns-enrollment-id=learn.wwl.set-up-configure-financial-management-work-general-ledger

Options tab on module for selection


WORKSPACES
________
1. Workspace is a one stop-shop for specific activities.
2. 360-degree view of activities : No need to navigate to multiple list
3. Answer specific questions  : Questions such as : 
        Are there urgent cases that need to be attended
        How difficult will my workload be ? 
        Are cases easy or difficult to solve ?
4. Provide insight : Compare multiple sources of data. Provide a big picture view that might be difficult to achieve when only looking at lists in specific modules.
5. Navigates by data : Less time spent filtering to find results
6. Direct access to tasks: Tasks can be performed directly from the workspace


*Customer Payment module


##### Legal Entity 

A legal entity is usually called the company organization branches. They are the list of available companies or branches within the Company or Organization.

![legal entities](Images/legalEntities.png)

We can also change the company image, logo, address etc there too. So go through the sub tabs.

###### Sequence Number Definition 

It's a unique identifier for each record in the system such as Customers, Vendors, Transactions or other transaction within the System. So in general, number sequences in finance and operations apps are used to generate readable, unique identifiers for master data records and transaction records that require identifiers such as customers,vendors, sales orders, purchase orders or any other transactions within the system. 

Each module specific parameter page has a reference to the sequence number that is define for that specific module.

You should specify the scope for sequence numbers.
    - Shared : A single number sequence is used for all organizations. The Shared scope is available only for some references.
    - Legal Entity : A separate number sequence is used for each company.

It consists segments
   - Company
   - Constant 
   - Alphanumeric : # for incremental numbers , & for incremental letters
  

Number sequence can be continuous or non-continuous. A continuous number sequence can skip numbers but numbers will be used sequentially. 

![continous](Images/continous.png)

Continuous sequence numbers are not recommended as they have a large impact on system performance. Continuous number sequences are typically required for external documents such as purchase orders however continuous number sequences can adversely affect system response times because the system must request a number from a database every time that a new document or record is created. 

If you use a non-continuous sequence sequence, you can enable Pre-allocation on the performance tab on the number sequence page. New numbers are requested from DB only after the pre allocated quantity has been used. 

In case of a power failure, an application error or other unexpected failure, F&O apps cannot recycle numbers automatically for continuous number sequences. You can run the cleanup process manually to recover the lost numbers. 

![number sequencing](Images/numbersequence.png)

Each module have their own number sequence setup. See for Account Payable. 

![accounts payable ns](Images/accountpayablens.png)

To speed up setup it's better to use the Number Sequence Wizard to set up the number sequence as there are lots of sequence to setup in the System. 

![ns wizard](Images/nswizard.png)

##### GLOBAL ADDRESS BOOK

![global address book](Images/globaladdressbook.png)

The Global address book is a centralized repository for master data that must be stored for all internal and external persons and 
organizations that the company interacts with. So that means when an address changes the update only needs to be made in one place all the other associated records are updated automatically. 

Customers : Individuals or companies who purchase goods or services from your organization.   

Prospects : A party that might provide a service or benefits to a legal entity.  

Worker : A person who is assumed as an employee.  

Vendor : A party that supply products to one or more legal entities in exchange for payments.  

Competitor : A person or organization that provides goods or services similar to yours. 

Application : A person who makes a formal written request to work in an organization.  

Contact : A person inside or outside your organization that you have created in your organization.

>>> Organization Administration > Global Address Book

![Global Address Book](Images/global%20address%20book%20party.png)

We can click on the NEW to create a new party. 

If we decide to create the Vendor or Customer directly from the Accounts payable/receivable module, the corresponding party record is also created within the System in the Global Address Book.   


##### SECURITY MANAGEMENT IN D365F&O

![security role](Images/securityRoles.png)

Security Architecture in F&0
_____

![security architecture](Images/securityArch.png)   

Authorization grants access but Data security denies access from tables fields, rows in the database.

Data Security for specific tables is enforced by Application Object Server (AOS).  

Auditing of user sign in and sign out is enabled, which means that the system logs when a user signs in or out of the application.

A sign out is logged even if the user's session expires or ends. 

A system administrator or security administrator can access the audit logs by going to the User log page.

>> System Administration > Inquiries > User log   

#### ROLE 

D365F&O uses a ROLE based security architecture. That means users are assigned to security roles based on their responsibilities in the organization and their participation in business processes.

Role based security is aligned with the structure of the business, it means that users are assigned to security roles based on their responsibilities in the organization and their participation in business processes.

In Role based security access is not granted to individual users only to security roles. Users are assigned to Roles then the Admin grants access to the duties that the users in a Role performs. 

Duty correspond to parts of a business process. The Administrator assigns duties to security roles and not in program elements that users wants to use. A duty can be assigned to more than one role and in D365FO duties contains privileges.

For example, the Maintain bank transactions duty contains 
- the generate deposit slips and 
- cancel payments privileges.

Both duties and privilege can be assigned  to security roles. However, it is recommended that you use duties to grant access to finance and operations apps. 

A Privilege specifies the level of access that is required to perform a job, solve a problem or complete an assignment. It also contains permissions to individual application objects such as user interface elements and tables.

For examples, the Cancel payments privilege contains permissions to the menu items, fields and tables that are required to cancel payments. 

By default, privileges are provided for all features in finance and operations apps. The Admin can modify the permissions that are associated with the privilege or create new privileges. 

Permission represents the access to individual objects such as menu items, tables , forms , services or reports.

![sec roles](Images/sec%20roles%20.png)

Each function in FO apps such as a form or a service, is accessed through an entry point.

Entry Point : Menu items, web content items and service operations are referred to collectively as entry points. 