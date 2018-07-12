This is an simple exercise used to filter interview candidates by assessing your approach to development and use of
infrastructure as code tooling. This has been tested using Terraform v0.11.3 we advise you use 
this version as we will test your code with the same. If you're reading this you've probably been forwarded here by an
agent to complete the exercise, if you do fork the repo please don't push your changes as they will be publicly visible
to any other candidates, instead zip up your repo and forward to the agent.

Here we have a Terraform script building a simple VPC network, for now we have just one instance running the web server 
Nginx in it's default configuration, serving up the default welcome page. To run this use the following command...

    terraform apply -var-file=dublin.tfvars

We want this to be extended, you're are tasked with making the alterations detailed below, after completing each stage 
a test to show the things are still working would be to run the following command and expect to see the Nginx welcome 
page HTML. (It may take some time for the server to be up and running after terraform completes)

    terraform output nginx_domain | xargs curl
    
Complete exercises 1-3, it is advisable to commit often, please don't submit just one commit we want to see an understanding 
of version control tooling. You are not expected to complete 4a or 4b as these tasks are more involved and we value your 
time, however if you have time to and would like to then please do implement just one of them. Alternatively you may 
begin to implement one and not complete it, you won't be marked down for this, leave TODO comments where appropriate 
and/or document how you would implement the task had you the time in a text file called notes.txt in the repository root.

1. We want to be able to run the same stack closer to our customers in the US. Please build the same stack in 
the us-east-1 (Virginia) region. Note that Virginia has serveral availability zones which we want to use 4 of them so 
that will need to be taken into consideration yet we still want to run a stack in Ireland using the 3 AZs there. We want
to reuse as much code as possible, we don't want a separate network definition for each region. Feel free to 
modify the existing code as much as possible in order to do this, you'll also need to consider terraform state each stack
should have it's own state but don't feel you need to go as far as setting up remote state. As for a CIDR block for the 
VPC use whatever you feel like, providing it's compliant with RFC-1918 and does not overlap with the dublin network.

2. The EC2 instance running Nginx went down over the weekend and we had an outage, it's been decided that we need a solution 
that is more resilient than just a single instance. Please implement a solution that you'd be confident would continue 
to run in the event one instance goes down. 

3. We are looking to improve the security of our network we've decided we need a bastion server to avoid logging on 
directly to our servers. Add a bastion server, the bastion should be the only route to SSH onto any server in the 
entire VPC.

4. a) The team have decided to use the Java framework Spring Boot to build features for our website. Deploy the following sample 
application into the VPC, reconfigure Nginx as a reverse proxy to the Java app. Provide a modification to the Terraform 
output/curl command to get the hello world text that the application serves. 
https://github.com/spring-projects/spring-boot/tree/master/spring-boot-samples/spring-boot-sample-tomcat
<br> b) Follow the instructions in a) but instead deploy the following application, with an alteration to use an Amazon 
RDS managed database rather than the default H2 in memory database. 
https://github.com/spring-projects/spring-boot/tree/master/spring-boot-samples/spring-boot-sample-data-jpa


