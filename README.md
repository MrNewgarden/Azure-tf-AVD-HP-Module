# Azure-tf-AVD-HP-Module
### This module deployes the following resources:
- 1 and only 1 Azure Virtual Desktop Hostpool
- Application groups, with workspacce attachment to the created AVD HP and 1 Entra ID group per application to provide access to remote desktop application for users. The ammount of application groups, etc. that will be deployed is decided in the "apps" key-value pair, see example!

### This module does NOT deploy the following resources:
- Storage account for FSLogix/profiles
- Virtual machine
- Probably something else ive forgotten to add


## Customizable module properties 

rdp_properties 
  description = RDP hostpool properties, also has a "ignore lifecycle change" tag on it, as scaling plans would not update the code..
  default     = audiocapturemode:i:1;audiomode:i:0;redirectprinters:i:1;drivestoredirect:s:c\\:;autoreconnection enabled:i:1;enablerdsaadauth:i:1;use multimon:i:1;dynamic resolution:i:1;networkautodetect:i:1
  

maximum_sessions_allowed 
  type        = number
  description = Maximum hostpool sessions allowed on session hosts in host pool
  default     = 10


type 
  description = What hostpool type to use in the hostpool
  default     = Pooled


load_balancer_type 
  description = Acceptable values are: BreadthFirst, DepthFirst or Persistent
  default     = DepthFirst


security_enabled 
  description = Whether the group is a security group for controlling access to in-app resources. At least one of security_enabled or mail_enabled must be specified. A group can be security enabled and mail enabled
  default     = true


start_vm_on_connect 
  type        = bool
  description = Start the VM on connect if no available sessions
  default     = true


location 
  description = Where will the host pool be deployed
  default     = West Europe


root_name 
  description = Should be a unique identifier, short name for a customer, project or something
  default     = csn


subscription_id 
  description = Subscription ID where virtual machine sessions hosts are located, this should be it's own subscription ID in production environments
  default     = null


apps 
  type        = map(string)
  description = Name of apps that will be deployed in a key value pair for each app
  default = 
    key = value
  


hostpool 
  description = Name of hostpool that will be deployed
  default     = prod-01


validate_environment 
  type        = bool
  description = Wether to validate environment or not
  default     = false


create_scaling_plan 
  type        = bool
  description = true or false if you want to create scaling plan and attach to the host pool
  default     = false


avd_displayname 
  description = Display name of Azure Virtual Desktop Enterprise application in Entra ID
  default     = Azure Virtual Desktop

