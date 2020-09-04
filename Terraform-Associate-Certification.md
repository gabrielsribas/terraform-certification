# Guia de estudo para obtenção da certificação hashicorp terraform associate.  

Outras informações  
https://learn.hashicorp.com/terraform  

State - Guardar e gerenciar o estado do arquivo terraform.tfstate. Assim é possível ter multiplas alterações e por times diferentes. O Terraform irá locar ()  
https://www.terraform.io/docs/state/index.html  

Review sobre a certificação  
https://learn.hashicorp.com/terraform/certification/terraform-associate-review  

Study Guide  
https://learn.hashicorp.com/terraform/certification/terraform-associate-study-guide  

Sample Questions  
https://learn.hashicorp.com/terraform/certification/terraform-associate-sample-questions  

Videos explicativos  
HashiCorp Certified Terraform Associate - Overview  
https://www.youtube.com/watch?v=vhZEdqlXlSs  

# QUASE UM DUMB Questions *** TestKing ???  
https://testmozusercontent.com/q/1245195/student  


# Questions  

Playlist questions terraform associate:  
HashiCorp Certified Terraform Associate - Overview  
https://www.youtube.com/watch?v=vhZEdqlXlSs&list=PL5VXZTK6spA2HF5Kf0rI9RDRHF9Hopffr  


1> https://www.terraform.io/docs/state/index.html  
Your manager has instructed you to start using terraform for your day-to-day operations , but your security team is concerned about the terraform state files . They have heard it contains confidential information , and are worried that it will not be securely protected. What should be your response to the security team in this regard?  

A. Inform the security team that using terraform state is optional . There are ways to avoid it , and you will do the same.  

B. Ensure them that terraform state does not contain any secrets/confidential data , so it should not be a problem if it is shared or available to public.  

C. Keep the state file locally on each developer machine , and ensure that there is a local protection software like KeyPass protecting it.  

D. Mask the confidential entries in the terraform state file , using Vault Enterprise, another Hashicorp product , while keeping it locally.  

>>>E. Ensure that the state is managed in a remote backend , preferably an enterprise grade state management system like Terraform Cloud  

2> https://www.terraform.io/docs/state/workspaces.html  
Your manager has instructed you to start using terraform for the entire infra provisioning of the application stack. There are 4 environments – DEV , QA , UAT , and PROD. The application team has asked for complete segregation between these environments including the backend , state , and also configurations ,since there will be unique resources in different environments . What is the possible way to structure the terraform code to facilitate that.  

A. Implement terraform workspaces , and map each environment with one workspace.  

B. Enable remote backend storage . Configure 4 different backend storages , one for each environment.  

>>>C. Completely separate the working directories , keep one for each environment . For each working directory , maintain a separate configuration file , variables file , and map to a different backend.  

D.  Completely separate the working directories , keep one for each environment . For each working directory , maintain a separate configuration file , variables file , and map to the same backend.  

3> https://www.terraform.io/docs/commands/taint.html  
   https://www.terraform.io/docs/commands/state/index.html  
While running a particular terraform script , you came across a problem – one of the resources got created incorrectly , and resulted in the resource being in a peculiar stage . As a result , you want terraform to delete it and recreate it again , but since it is already stored in terraform state , on running plan again , no differences are being observed . What is the most efficient way to handle this particular use-case?  

A. Destroy the resource manually from the corresponding CSP/infra services portal ,and then run terraform apply command again.  

B. Run terraform state rm command with that particular resource id to remove it from the state , and then run the terraform apply command again.  

C. This is not possible in the Open source version , you need to use Terraform Cloud / Terraform enterprise for this.  

D.  Run terraform destroy with –target command to destroy the resource first , then run terraform apply on the subsequent run.  

>>>E. Run terraform taint command with the resource ID of the particular problematic resource . This will mark this resource for subsequent deletion , and recreation in the next terraform apply cycle.  

4> https://www.terraform.io/docs/modules/composition.html  
Your application team resources want to contribute to IaC coding practices . They want you to refactor your code to be reusable , and wants you to create as many modules as possible , along with 3-4 levels of child modules , and also modules as wrappers for even simple resource types. What should your response be to the above?   

A. You should agree and create as many modules as requested based on their inputs.  

B. You will partially agree , and inform them that as per terraform best practices , module nesting should not be more than 5 levels.  

>>>C. You should reject their request , and tell them that rather module composition should be used . Module nesting should not be more than 1 level , and also , modules should not be simple wrappers around basic resources.  

D.  You should reject their request saying that modules should only be created for exceptional cases , and avoided for normal cases.  

E. You should agree , and inform them that in case they need to pass values across modules , they should use terraform state .  

5> https://www.terraform.io/docs/cloud/registry/index.html  
Your company has been using Terraform Cloud for a some time now . But every team is creating their own modules , and there is no standardization of the modules , with each team creating the resources in their own unique way . You want to enforce a standardization of the modules across the enterprise . What should be your approach.  

A. Upgrade to Terraform enterprise , since this is not possible in terraform cloud.  

>>>B. Implement a Private module registry in Terraform cloud , and ask teams to reference them.  

C. Upload the modules in the terraform public module registry , and ask teams to reference them.  

D.  Create individual workspaces for each team , and ask them to share modules across workspaces.  

E. Use module composition to use the same module across all projects , and workspaces  

6> https://www.terraform.io/docs/configuration/resources.html#depends_on-explicit-resource-dependencies  
```
   resource "aws_s3_bucket" "example" { 
   bucket = "my-test-s3-terraform-bucket"
   …} 
resource "aws_iam_role" "test_role" { 
   name = "test_role"
   …}
```   
Due to the way that the application code is written , the s3 bucket must be created before the test role is created , otherwise there will be a problem. How can you ensure that?  

A. Create 2 separate terraform config scripts , and run them one by one , 1 for s3 bucket , and another for IAM role , run the S3 bucket script first.  

B. This will already be taken care of by terraform native implicit dependency. Nothing else needs to be done from your end.  

>>>C.  Add explicit dependency using depends_on . This will ensure the correct order of resource creation.  

D. This is not possible to control in terraform . Terraform will take care of it in a native way , and create a dependency graph that is best suited for the parallel resource creation.  

7> https://www.terraform.io/docs/configuration/terraform.html#specifying-a-required-terraform-version  
You have created a terraform script that uses a lot of new constructs that have been introduced in terraform v0.12 . However , many developers who are cloning the script from your git repo , are using v0.11 , and getting errors , and raising hundreds of tickets. What can be done from your end to solve this problem?  

A. Refactor the code to support both v0.11 , and v0.12 . It might be a difficult process , but there is no other way.  

B. Add a condition in front of each such specific construct , to check whether the running terraform version id v0.11 or v0.12 , and ,work accordingly.  

C.  Add comments in your code to tell developers to use v0.12 . If they use v0.11 , that should be their problem , which they need to figure out.  

>>>D. Use the terraform setting ‘required_version’ and set it to &gt;=0.12 . This will ensure that developers are forced to use v0.12 , and does not use anything else.  

8> https://www.terraform.io/docs/commands/console.html  
Your developers are facing a lot of problem while writing complex expressions involving difficult interpolations . They have to run the terraform plan every time and check whether there are errors , and also check terraform apply to print the value as a temporary output for debugging purposes. What should be done to avoid this?  

A. Use terraform zipmap function , it will be able to easily do the interpolations without complex code.  

B. Add a breakpoint in your code, using the watch keyword , and output the value to console for temporary debugging.  

>>>C.  Use terraform console command to have an interactive UI with full access to the underlying terraform state to run your interpolations , and debug at real-time.  

D. Use terraform console command to have an interactive UI , but you can only use it with local state , and it does not work with remote state.  

9> https://www.terraform.io/docs/import/index.html  
Your company has a lot of workloads in AWS , and Azure that were respectively created using CloudFormation , and AzureRM Templates. However , now your CIO has decided to use Terraform for all new projects , and has asked you to check how to integrate the existing environment with terraform code. What should be your next plan of action?  

A. Tell the CIO that this is not possible . Resources created in CloudFormation , and AzureRM templates cannot be tracked using terraform.  

B. This is only possible in Terraform Enterprise , which has the TerraformConverter exe that can take any other template language like AzureRM and convert to Terraform code.  

C.  Just write the terraform config file for the new resources , and run terraform apply , the state file will automatically be updated with the details of the new resources to be imported.  

>>>D. Use terraform import command to import each resource one by one .  

10> https://www.hashicorp.com/products/terraform/pricing  
Please identify the offerings which are unique to Terraform Enterprise , and not available in either Terraform OSS , or Terraform Cloud. There can be more than one answer.  

>>>A. SAML/SSO.  

B. Sentinel.  

>>>C. Audit Logs.  

>>>D. Private Network Connectivity.  

E. Full API Coverage.  

F. VCS Integration.  

>>>G. Clustering.  

11> https://www.terraform.io/docs/cloud/sentinel/index.html  
Your team lead does not trust the junior terraform engineers who now have access to the git repo . So , he wants you to have some sort of a checking layer , whereby , you can ensure that the juniors will not create any non-compliant resources that might lead to a security audit failure in future. What can you do to efficiently enforce this ?   

A. Create a git master branch , and implement PR . Every change needs to be reviewed by you , before being merged to the master branch.  

B. Create a design /security document (in PDF) and share to the team , and ask them to always follow that document , and never deviate from it.  

>>>C. Since your team is using Hashicorp Terraform Enterprise Edition , enable Sentinel , and write Policy-As-Code rules that will check for non-compliant resource provisioning , and prevent/report them.  

D. Use Terraform OSS Sentinel Lite version , which will save cost , since there is no charge for OSS , but it can still check for most non-compliant rules using Policy-As-Code  

12> https://www.terraform.io/docs/configuration/providers.html#alias-multiple-provider-instances  
Your team has started using terraform OSS in a big way , and now wants to deploy multi region deployments (DR) in aws using the same terraform files . You want to deploy the same infra (VPC,EC2 …) in both us-east-1 ,and us-west-2 using the same script , and then peer the VPCs across both the regions to enable DR traffic. But , when you run your script , all resources are getting created in only the default provider region. What should you do?  

Your provider setting is as below-  

**The default provider configuration**  
```
   provider "aws" {
   region = "us-east-1"
} 
```  
A. No way to enable this via a single script . Write 2 different scripts with different default providers in the 2 scripts , one for us-east , another for us-west.  

B. Manually create the DR region , once the Primary has been created , since you are using terraform OSS , and multi region deployment is only available in Terraform Enterprise.  

>>>C. Use provider alias functionality , and add another provider for us-west region . While creating the resources using the tf script , reference the appropriate provider (using the alias).  

D. Create a list of regions , and then use a for-each to iterate over the regions , and create the same resources ,one after the one , over the loop.  

13> https://www.terraform.io/docs/commands/init.html  
Terraform has a standard way of doing things . It is always best to follow the standard way , and not deviate from it , to make sure that you use the tool most efficiently. For example , one of the best practices of using terraform is to run terraform init only twice , once at the beginning of the project , and once at the end. Multiple terraform init calls in succession should be avoided since they can result in inconsistencies of your terraform state file . Please share your views on the above statement.  

A. Yes , the above statement is completely correct . Terraform init should be run very carefully , since every terraform init run cannot adversely affect the state file , if proper precautions are not taken.  

>>>B. The above statement is absolutely wrong . Terraform init has no dependency with state , and can be run as many time , and in whatever frequency as needed . It is an idempotent operation , and as such does not alter anything.  

C. The above statement is only partially correct . Terraform init can indeed be run only a few times , but that is not due to any issue with state alteration , but because , everytime terraform init will initiaitlize the project , and download all plugins from the internet repository , regardless of whether they were present or not , and this increases the waiting time.  

14> https://www.terraform.io/guides/core-workflow.html  
What is the standard workflow that a developer follows while working with terraform , on a standard IaC project , when using Terraform OSS  

>>>A. Write the terraform code on the developer machine , run terraform plan to check the changes , and run terraform apply to provision the infra.  

B. Run terraform refresh to update the terraform state , then write the terraform code , and finally run terraform apply.  

C. Run terraform destroy first since you need to start from fresh every time , before running terraform apply.  

D. Write terraform code , and run terraform push , to update the terraform state to the remote repo , which in turn will take care of the next steps.  

15> https://www.terraform.io/docs/commands/fmt.html  
What terraform command can enable syntax level formatting , and consistent canonical style across all terraform code?  

A. Run terraform style –enable command to apply a consistent layout/formatting to each terraform script file.  

B. Run terraform fmt command at the root directory , and it will apply consistent formatting to all files in that root directory ,and any nested child directories.  

C. This is only possible in the Terraform Enterprise version ( Team & Governance package) , not available in OSS as of now .  

>>>D. Run terraform fmt , but with the –recursive flag enabled , to ensure that all child directories are also properly formatted , along with the parent directory.  

16> https://www.terraform.io/docs/state/locking.html  
        https://www.terraform.io/docs/backends/types/s3.html  
You have 5-7 developers working on your terraform project (using terraform OSS), and you saved the terraform state in a remote S3 bucket . However , sometimes you are observing inconsistencies in the provisioned infrastructure / failure in the code . You have traced this problem to simultaneous/concurrent runs of terraform apply command for 2/more developers . What can you do to fix this problem ?   

A. Structure your team in such a way that only one individual will run terraform apply , everyone will just make changes and share with him. Then there will be no chance of any inconsistencies.  

B. Stop using remote state , and store the developer tfstate in their own machine . Once a day , all developers should sit together and merge the state files manually , to avoid any inconsistencies.  

C. Use terraform workspaces feature, this will fix this problem by default , as every developer will have their own state file , and terraform will merge them on server side on its own.  

>>>D. Enable terraform state locking for the S3 backend using DynamoDB table. This prevents others from acquiring the lock and potentially corrupting your state.  

17> https://www.terraform.io/docs/registry/modules/use.html  
       https://registry.terraform.io  
Your team uses terraform OSS . You have created a number of resuable modules for important , independent network components that you want to share with your team to enhance consistency . What is the correct option/way to do that?  

A. Terraform modules cannot be shared in OSS version . Each developer needs to maintain their own modules , and leverage them in the main tf file.  

B. Terraform module sharing is only available in Enterprise version via terraform private module registry , so no way to enable it in OSS version.  

C. Store your modules in a NAS/ shared file server , and ask your team members to directly reference the code from there . This is the only viable option in terraform OSS ,which is better than individually maintaining module versions for every developer.  

>>>D. Upload your modules with proper versioning in the terraform public module registry . Terraform OSS is directly integrated with the public module registry , and can reference the modules from the code in the main tf file.  

18> https://www.terraform.io/docs/internals/debugging.html  
You have written a terraform IaC script which was working till yesterday , but is giving some vague error from today , which you are unable to understand . You want more detailed logs that could potentially help you troubleshoot the issue , and understand the root cause. What can you do to enable this setting? Please note , you are using terraform OSS.  

A. Terraform OSS can push all its logs to a syslog endpoint . As such , you have to set up the syslog sink , and enable TF_LOG_PATH env variable to the syslog endpoint and all logs will automatically start streaming.  

B. Detailed logs are not available in terraform OSS , except the crash message . You need to upgrade to terraform enterprise for this point.  

C. Enable the TF_LOG_PATH to the log sink file location , and logging output will automatically be stored there.  

>>>D. Enable TF_LOG to the log level DEBUG , and then set TF_LOG_PATH to the log sink file location . Terraform debug logs will be dumped to the sink path ,even in terraform OSS  

19> https://www.terraform.io/docs/commands/refresh.html  
What does terraform refresh command do ?  

A. terraform refresh can be used to selectively update sections of the state file , using terraform resource level addressing.  

B. terraform refresh command basically updates the code file with the current state of the target infrastructure .  

C. terraform refresh is use to change/modify the infrastructure based on the existing state file , at that moment.  

>>>D. terraform refresh syncs the state file with the real world infrastructure. It does not affect the actual target infra / the terraform code file in any fashion.  

20> https://www.terraform.io/docs/internals/resource-addressing.html  
Given the below resource configuration -  
```
resource "aws_instance" "web" {
   # ... 
   count = 4 
} 
``` 
What does the terraform resource address ‘aws_instance.web’ refer to?  

A. It refers to the first web EC2 instance out of the 4 ,as by default , if no index is provided , the first / 0th index is used.  

>>>B. It refers to all 4 web instances , together , for further individual segregation , indexing is required , with a 0 based index.  

C. It refers to the last web EC2 instance , as by default , if no index is provided , the last / N-1 index is used.  

D. The above will result in a syntax error , as it is not syntactically correct . Resources defined using count , can only be referenced using indexes.  


# Guia para estudo. Direto ao ponto - Documentação  
https://adinermie.com/hashicorp-certified-terraform-associate-study-guide/  


# Outras anotações importantes:  
- Melhor definição para first-class  
https://stackoverflow.com/questions/245192/what-are-first-class-objects  

- State file is always encrypted at rest. T/F:  
   . False  

- In Terraform 0.12, you can do:  
```   
   variable "myvar" {
   type = string
   }
``` 
   ..Note: string does not have any quotes around it. This is possible because:  
1)Types are always complex  

>>2) Types are first class values  

3) Types are string only  

4) Types are second-class values  

- Can you depends_on parameter with data block?  
   . yes  
- Workspace functionality is same between terraform cloud, terraform enterprise, and terraform opensource.  
   . false  
- Resource Graph:   
   . São alterações e dependências. Landscape  
- If there are multiple .tf files, how will terraform "load" them?  
   . alphabetical order  
- Terraform é uma linquagem declarativa.  
- Get resource list from terraform state  
   . terraform state list  
- One way to define variables to be used in the child module and give them default values:  
   . Put them in a .tfvars file in the MODULE directory and give them default values  
- Dynamic block acts like a :  
   . for loop  
- Terraform Cloud can be managed by CLI, but it needs:  
   . API Token  
- Most common place where people save remote state files?  
   . s3 bucket  
- Terraform cannot manage cross-cloud dependencies:  
   . false  
- Map definition format:  
   . foo = {}  
- To publish to Terraform's public module registry name has to be in ___________ format:  
   . terraform-<PROVIDER>-<NAME>  
- Splat expressions use which character?  
   . *  
- In Terraform 0.12, you can return the entire module itself from a module.  
   . Yes  
- PTFE is same as:  
   . Terraform Enterprise  
- If you only have one folder of terraform codes, you are using _____________________ module:  
   . root  
- Count has 2 limitations (1. inline and 2. modifications in code creates unexpected results) in Terraform 0.11. Which expression in Terraform 0.12 solves this problem?  
   . for_each  
- Which of the following is NOT a component of Terraform  
   . libraries  
- State file should be kept secret since it has sensitive data:  
   . True  
- Which feature allows to store modules ONLY for your organization?  
   . Private Module registry  
- There are providers for which of the following?  
   . docker, aws e azure  
- With terraform init command , if you want to key/value directly on the command line, what does that look like?  
   . -backend-config="KEY=VALUE"  
- In this command: what does upgrade do? terraform init -upgrade  
   . upgrades modules and providers  
- Command to create a new workspace named foo  
   . terraform workspace new foo  
- This is an example of:  
```
      terraform {
         backend "s3" {
            # (backend-specific settings...)
         }
      }
``` 
   . terraform block  
- You can use count to loop over an entire resource and you can also use count within a resource to loop over inline blocks. True/False.  
   . True  
- Which of the following is NOT a type of collections:  
   . Object  
- Inside a module what do you use so that a variable or attribute's value is available to the caller terraform code?  
   . output  
- In Terraform Enterprise, each workspace can map to how many VCS repos(s)?  
   . 1  
- _________ is a special provider that exists to provide an interface between Terraform and external programs  
   . external  
- Adding in explicit provider dependency in provider block is not a good practice.  
   . false  
- Which type does the length function not work on?  
   . number  
- You have 2 folders of terraform code. Both folders save their state remotely on a s3 bucket. If you want to access resources of folder2 from folder1 , what do you have to do?  
   . point to it using data "terraform_remote_state" block  
- It is secure practice to omit secrets when storing state in the backend. Given that's done, can you use  -backend-config=PATH to specify secrets when trying communicate with the backend?  
   . Yes  
- What is the result of this:  
   > zipmap (["foo", "bar"], [5, 10])  
   . { "foo" = 5  
       "bar" = 10 }  
   OBS.: Estudar sobre o zipmap  

- In Terraform 0.12 , which of the following is true?  

   1) Parent module can not send complex objects to child module, but child module can return complex objects  

   2) Parent module can not send complex objects to child module AND child module cannot return complex objects  

   3) Parent module can send complex objects to child module, but child module cannot return complex objects  

   >>4) Parent module can send complex objects to child module, AND child module can return complex objects  

- Plugins execute as separate processes:  
   . Verdade  

- Which of the following is NOT valid way to enter comments in terraform code:  
   1) /*.  */  

   >>2) /.      ./  

   3) #  

   4) //  

- The following is an example of ___________:  
```
   dynamic "ingress" {
      for_each = var.foo_ports
      content {
         from_port = ingress.value
         to_port = ingres.value
         protocol = "tcp"
      }
``` 
   >>1) Dynamic Block  

   2) Dynamic backend  

   3) Dynamic Provisioning  

   4) Terraform block  

- You have file foo.tf with 5 resources defined in it. You also bar.tf with another 5 resources defined in it. If concatenate the 2 files and deleted foo.tf bar.tf files, what would be the impact?  

1) You will get an error because terraform will look for those 2 files.  

2) You will have to do terraform init all over again  

3) Terraform plan will be fine, but terraform apply will report an error  

>>4) Nothing  

## Principal terraform workspace commands easier:  
- terraform13 workspace [new, list, show, select, delete]  


# Learn about IaC  
## Infrastructure as Code: What Is It? Why Is It Important?  
   . O valor no `o que é `e `porque é importante` iac está na capacidade versionamento, reusabilidade e automação da infraestrutura.  

## Infrastructure as Code in a Private or Public Cloud.  
   . A ideia aqui seria o entendimento em relação a cloud privada em detrimento a cloud pública.  
      > Manter uma cloud privada exige muita expertise de soluções individuais.  
      > As equipes normalmente são grandes e as alterações, apesar de terem um nível de automação e alta disponibilidade, seguem um estilo próprio de configuração e proviosamento de infraestrura.  
      > Normalmente, as alterações são realizadas na cara do sistema via CLI e/ou GUI, levando ao risco de imperícia, mismatch de configurações, etc...  
      Final.: O iac vem para cobrir esses gaps. Fornecendo infraestrutura gerenciável, automatizada, versionada, workflow padronizado, código legível, etc...  
              Repositórios como github, gitlab, bitbucket, etc.. Normalmente são utilizados como a fonte de verdade e são ligados em ferramentas de CI para realizarem testes na infraestrutura antes de aplicar qualquer coisa.  
              O terraform resolve esse problema, deixando as alterações de infraestrutura preditíveis, idempotente. Uma vez que além de liberar para aplicação das alterações no ambiente após os testes (plan) rodarem com sucesso. Te dá um breaf sobre como está o estado da sua infraestrura em constraste ao que está se propondo a aplicar. E aplicando apenas a diferença proposta.  

## Introduction to Terraform  
   . Terraform provê um plano de execução. Isso quer dizer que antes de aplicar qualquer coisa ele planeja sua execução.  
   . Terraform executa e aplica seu plano de forma paralela para recursos que são independentes.  
   . Terraform te conta o que está alterando(add, change, destroy) e em qual ordem.  
   .  

## Casos de uso  
   . São demonstração da aplicabilidade do terraform em vários cenários e arquiteturas. Alguns exemplos são:  
      > heroku webapp  
      > Arquitetura de aplicação multicamada. Ex.: A camada de banco de dados é criada antes da camada web, etc...  
      > Multi-cloud deployments. Fazer deployments em diferentes providers cloud. O terraform é cloud-agnostic.  
      > SDN.  
      > etc...  

# Manage infrastructure   

https://learn.hashicorp.com/tutorials/terraform/associate-study  
...Continuar em >> Learn more subcommands  



#APPENDICE:  
   . version control system (VCS)  
