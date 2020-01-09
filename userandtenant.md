# Tenant
- tenant is for b2b 
- tenant have its own branchs thoese are sub tenants

**Tenat**[Table]

    public partial class Tenant : BaseEntity
    {

        /// <summary>
        /// Gets or sets the ParantTenant 
        /// </summary>
        public long ParantTenantId { get; set; }

        /// <summary>
        /// Gets or sets the Tenant name
        /// </summary>
        public string Name { get; set; }

        /// <summary>
        /// Gets or sets the Tenant IsActive
        /// </summary>
        public bool IsActive { get; set; }

    }

**Example Tenant Data**

| Id 	| ParantTenantId 	| IsActive 	| Name          	| CreatedOnUtc 	| UpdatedOnUtc 	| CreatedUserId 	| UpdatedUserId 	|
|----	|----------------	|----------	|---------------	|--------------	|--------------	|---------------	|---------------	|
| 1  	| 1              	| true     	| OTA           	|              	|              	| 1             	| 1             	|
| 2  	| 1              	| true     	| krishna-all   	|              	|              	| 1             	| 1             	|
| 3  	| 2              	| true     	| krishna-delhi 	|              	|              	| 1             	| 1             	|
| 4  	| 2              	| false    	| krishna-viz   	|              	|              	| 1             	| 1             	|


# User
- user have both b2b and b2c
- user have b2c is default tenant **OTA** ,if user have b2b has assigned tenant.

**User**[Table]

    public partial class User: BaseEntity
    {
        /// <summary>
        /// Gets or sets the Tenant 
        /// </summary>
        public long TenantId { get; set; }

        /// <summary>
        /// Gets or sets the UserName 
        /// </summary>
        public string UserName { get; set; }

        /// <summary>
        /// Gets or sets the PasswordSolt 
        /// </summary>
        public string PasswordSolt { get; set; 
        }

        /// <summary>
        /// Gets or sets the SoltKey 
        /// </summary>
        public string SoltKey { get; set; 
        }

        /// <summary>
        /// Gets or sets the FirstName 
        /// </summary>
        public string FirstName { get; set; 
        }

        /// <summary>
        /// Gets or sets the LastName 
        /// </summary>
        public string LastName { get; set; 
        }

        /// <summary>
        /// Gets or sets the Email 
        /// </summary>
        public string Email { get; set; 
        }

        /// <summary>
        /// Gets or sets the IsSocial 
        /// </summary>
        public bool IsSocial { get; set; 
        }

        /// <summary>
        /// Gets or sets the SocialName
        /// </summary>
        public SocialEnum SocialName { get; set; 
        }

        /// <summary>
        /// Roles forienKey relations
        /// </summary>
        public virtual ICollection<UserCustumerRoles> UserCustumerRoles { get; set; 
        }

    }

**UserCustomerRole**[Table]

    public partial class UserCustomerRoles
    {
        public long Userid{get;set;}
        public long CustomerRoleId{get;set;}
    }


**SocialEnum**[Enum]

    public Enum SocialEnum
    {
        Google=1,
        Facebook=2,
        Twitter=3
    }



**Example User Data**

| Id 	| TenantId 	| UserName   	| PasswordSolt 	| SoltKey 	| FirstName 	| LastName 	| Email              	| IsSocial 	| SocialName 	| CreatedOnUtc 	| UpdatedOnUtc 	| CreatedUserId 	| UpdatedUserId 	|
|----	|----------	|------------	|--------------	|---------	|-----------	|----------	|--------------------	|----------	|------------	|--------------	|--------------	|---------------	|---------------	|
| 1  	| 1        	| superadmin 	| xxxx         	| xxxx    	| super     	| admin    	| sadmin@gmail.com   	| false    	|            	|              	|              	| 1             	| 1             	|
| 2  	| 2        	| bb_admin   	| xxxx         	| xxx     	| admin     	| bb       	| b2bAdmin@gmail.com 	| false    	|            	|              	|              	| 1             	| 1             	|


**Example UserCustomerRole Data**

| Id 	| Userid 	| CustomerRoleId 	| CreatedOnUtc 	| UpdatedOnUtc 	| CreatedUserId 	| UpdatedUserId 	|
|----	|--------	|----------------	|--------------	|--------------	|---------------	|---------------	|
| 1  	| 1      	| 1              	|              	|              	| 1             	| 1             	|
| 2  	| 2      	| 3              	|              	|              	| 1             	| 1             	|