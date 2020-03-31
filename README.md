This is an exercise used to filter interview candidates by assessing your approach to development and use of
infrastructure as code tooling. This has been tested using terraform v0.12.24 we advise you use 
this version as we will test your code with the same. If you're reading this you've probably been forwarded here by an
agent to complete the exercise, if you do fork the repo please don't push your changes as they will be publicly visible
to any other candidates, instead zip up your repo and forward to the agent.

Here we have some terraform to build a simple VPC network, for now we have just one instance running the web server 
Nginx in it's default configuration, serving up the default welcome page. To run this use the following command...

    terraform apply -var-file=dublin.tfvars

We want this to be extended, you're tasked with making the alterations detailed below, after completing each stage 
a test to show the things are still working would be to run the following command and expect to see the Nginx welcome 
page HTML. (It may take some time for the server to be up and running after terraform completes)

    terraform output nginx_domain | xargs curl
    
Complete exercises 1 & 2 at home, it is advisable to commit often, please don't submit just one commit we want to see an 
understanding of version control tooling. You are not expected to complete 3, 4 & 5 as these tasks are more involved and we 
value your time. However do think about how you would approach these as we may discuss them if and when we bring you in 
for interview.

1. We want to be able to run the same stack closer to our customers in the US. Please build the same stack in 
the us-east-1 (Virginia) region, leaving the existing one in place too.  Feel free to modify the code and or structure 
as much as needed in order to do this, you'll need to consider terraform state each stack should have it's own state but 
don't feel you need to go as far as setting up remote state. As for a CIDR the new VPC use whatever you feel like, 
providing it's compliant with RFC-1918 and does not overlap with the dublin network.

2. Virginia has several availability zones, we want to use 4. Yet we still want to run the stack in Ireland using the 3 
AZs there. Modify the Virgina stack to span 4 AZs do this however you like, but consider that we would like to 
see reuse of code.

3. The EC2 instance running Nginx went down over the weekend, we had an outage, it's been decided that we need a solution 
that is more resilient than just a single instance. Please implement a solution that you'd be confident would continue 
to run in the event one instance goes down. 

4. We are looking to improve the security and segregation of our network we've decided we would like private subnets that
are not addressable on the internet. Modify the VPC to meet this requirement, the private subnets should still have egress
internet connectivity.

5. We'd like a bastion host, to enable SSH sessions to instances in the private subnets. Create this instance with associated
security groups. Even better would be an on-demand bastion, one that is spun up in the rare occasion an SSH session is needed.
How could this be defined in terraform?
 

