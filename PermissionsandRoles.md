# Permissions

- The permissions in the system is defined which actions have you autorized. 
- Group of permissions assiged to a role.
- Each Permission as one action with **CRUD** Access.

#### Table Schema of Permission table

**PermissionRecord**[Table]

    public partial class PermissionRecord : BaseEntity
    {
    
    /// <summary>
    /// Gets or sets the permission name
    /// </summary>
    public string Name { get; set; }

    /// <summary>
    /// Gets or sets the permission system name
    /// </summary>
    [Key(Unique=true)]
    public string SystemName { get; set; }

    
    /// <summary>
    /// Gets or sets foreign key Relation table CustomerRolesCrudAccess
    /// </summary>

    public virtual ICollection<CustomerRolesCrudAccess> CustomerRolesCrudAccess{get;set;}


**Example PermissionRecord Data**

| Id 	| Name              	| SystemName        	| CreatedOnUtc 	| UpdatedOnUtc 	| CreatedUserId 	| UpdatedUserId 	|
|----	|-------------------	|-------------------	|--------------	|--------------	|---------------	|---------------	|
| 1  	| Manage Booking    	| manage_booking    	|              	|              	| 1             	| 1             	|
| 2  	| Manage Paymanets  	| manage_paymanets  	|              	|              	| 1             	| 1             	|
| 3  	| Manage Users      	| manage_users      	|              	|              	| 1             	| 1             	|
| 4  	| Manage Tenants    	| manage_tenants    	|              	|              	| 1             	| 1             	|
| 5  	| Manage Refunds    	| manage_refunds    	|              	|              	| 1             	| 1             	|
| 6  	| Manage Promotions 	| manage_promotions 	|              	|              	| 1             	| 1             	|




**CustomerRolesCrudAccess**[Table]
    
    public class CustomerRolesCrudAccess:BaseEntity
    {
        public long PermissionId{get;set;}
        public long CustomerRoleId{get;set;}
        public CrudAccess CrudAccess{get;set;}
    }
**CrudAccess**[flag]

    [Flags]
    public enum CrudAccess
    {
        None = 0,
        Create = 1,
        Read = 2,
        Update = 4,
        Delete = 8,
        Listing = 16
    }


**Exmaple Data CustomerRolesCrudAccess**

| Id 	| PermissionId 	| CustomerRoleId 	| CrudAccess 	| CreatedOnUtc 	| UpdatedOnUtc 	| CreatedUserId 	| UpdatedUserId 	|
|----	|--------------	|----------------	|------------	|--------------	|--------------	|---------------	|---------------	|
| 1  	| 1            	| 1              	| 31         	|              	|              	| 1             	| 1             	|
| 1  	| 1            	| 1              	| 23         	|              	|              	| 1             	| 1             	|


**BaseEntity**[common base]

    public class BaseEntity
    {
        [Key]
        public long Id {get;set;}
        /// <summary>
        /// Gets or sets the date and time of  creation
        /// </summary>
        public DateTime CreatedOnUtc { get; set; }

        /// <summary>
        /// Gets or sets the date and time of  update
        /// </summary>
        public DateTime UpdatedOnUtc { get; set; }

        /// <summary>
        /// Gets or sets the userid of  creation
        /// </summary>
        public long CreatedUserId { get; set; }

        /// <summary>
        /// Gets or sets the userid of  update
        /// </summary>
        public long UpdatedUserId { get; set; }

    }


# Roles

- role is group of permissions
- roles of B2B by predefined with some roles , those b2b will assign new roles with their preference using our allowed b2b permissions

**CustomerRole**[Table]

        public partial class CustomerRole : BaseEntity
        {

        /// <summary>
        /// Gets or sets the customer role name
        /// </summary>
        public string Name { get; set; }

        /// <summary>
        /// Gets or sets a value indicating whether the customer role is active
        /// </summary>
        public bool Active { get; set; }

        /// <summary>
        /// Gets or sets a value indicating whether the customer role is system
        /// </summary>
        public bool IsSystemRole { get; set; }

        /// <summary>
        /// Gets or sets the customer role system name
        /// </summary>
        public string SystemName { get; set; }

        /// <summary>
        /// Gets or sets the TenantId ,it specify which Tenant
        /// </summary>
        public long TenantId { get; set; }

        /// <summary>
        /// Gets or sets foreign key Relation table CustomerRolesCrudAccess
        /// </summary>

        public virtual ICollection<CustomerRolesCrudAccess> CustomerRolesCrudAccess{get;set;}

    }



**Example CustomerRole Data**

| Id 	| Name        	| Active 	| IsSystemRole 	| SystemName  	| TenantId 	| CreatedOnUtc 	| UpdatedOnUtc 	| CreatedUserId 	| UpdatedUserId 	|
|----	|-------------	|--------	|--------------	|-------------	|----------	|--------------	|--------------	|---------------	|---------------	|
| 1  	| Super Admin 	| true   	| true         	| super_admin 	| 1        	|              	|              	| 1             	| 1             	|
| 2  	| Admin       	| true   	| true         	| admin       	| 1        	|              	|              	| 1             	| 1             	|
| 3  	| b2b Admin   	| true   	| true         	| b2b_admin   	| 1        	|              	|              	| 1             	| 1             	|
| 4  	| b2b custom  	| true   	| false        	| b2b_custom  	| 2        	|              	|              	| 1             	| 1             	|
