This is an exercise used to filter interview candidates by assessing your approach to development and use of
infrastructure as code tooling. This has been tested using terraform v0.14.5 we advise you use 
this version.

Here we have some terraform to build a simple VPC network, for now we have just one instance running the web server 
Nginx in its default configuration, serving up the default welcome page. To run this use the following command...

    terraform init && terraform apply -var-file=dublin.tfvars

We want this to be extended. You're tasked with making the alterations detailed below. After completing each stage, 
a test to show the things are still working would be to run the following command. Expect to see the Nginx welcome 
page HTML.

    terraform output nginx_domain | xargs curl


1. We want to be able to run the same stack closer to our customers in the US. Please build the same stack in 
the us-east-1 (Virginia) region, leaving the existing one in place too.  Feel free to modify the code and or structure 
as much as needed in order to do this, you'll need to consider terraform state each stack should have its own state but 
don't feel you need to go as far as setting up remote state. As for a CIDR the new VPC use whatever you feel like, 
providing it is compliant with RFC-1918 and does not overlap with the dublin network.

2. Virginia has several availability zones, we want to use 4. Yet we still want to run the stack in Ireland using the 3 
AZs there. Modify the Virgina stack to span 4 AZs do this however you like, but consider that we would like to 
see reuse of code.

3. The EC2 instance running Nginx went down over the weekend, we had an outage, it's been decided that we need a solution 
that is more resilient than just a single instance. Please implement a solution that you'd be confident would continue 
to run in the event one instance goes down. 

4. We are looking to improve the security and segregation of our network we've decided we would like private subnets that
are not addressable on the internet. Modify the VPC to meet this requirement, the private subnets should still have egress
internet connectivity.

5. In order to provide a consistent environment on the teams CI server and each engineer's workstation we've decided it 
would make sense to run terraform in Docker. Create a Dockerfile and a wrapper script that will enable this. THe script
should be callable with the same arguments as the terraform cli tool, i.e. init/plan/apply etc
 

