# Next-Generation Networking with AWS Transit Gateway

An announcement in AWS' networking space, the release of **AWS Transit Gateway** and the introduction of **Shared VPCs** has particularly caught my attention. AWS Transit Gateway is a truly game-changing technology solution as it provides a central hub for connecting AWS VPCs and VPN connections, while Shared VPC eases the pain of managing multiple VPCs by allowing you to centrally manage and distribute them to accounts in your organization.

![Welcome to Cable Hell](assets/transitgateway.jpg)

Considering the array of cutting-edge services at your fingertips within the AWS platform, it's fairly easy to understand why a core topic such as network architecture often draws less of a crowd, or the ire of most.

But answer me this: Would you build a new house without first knowing that the foundations were solid?

While I am amazed by AWS and their continued product releases in areas such as IoT, real-time data streaming and now even Satellite communication, I remain passionate about fundamental content such as multi-account strategies, governance at scale, and network architectures in the cloud. As a cloud architect, these are the foundations that pave the way for success in our respective journeys with Amazons cloud ecosystem.

I'll start by discussing the historical challenges of networking at scale in AWS, before outlining each service and discussing how I believe their combination will alter the design of foundational network architectures in AWS going forward.


### The Challenges of Networking at Scale in AWS

As organizations have moved to AWS in recent years, [Virtual Private Clouds](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html) (VPCs) have been identified as an ideal method for separating workloads from one another when necessary. Here's a quick refresher. A VPC allows you to provision a logically isolated section of the AWS cloud where you can launch resources in a virtual network that you define. In the scenario where resources within two separate VPCs require the ability to communicate, a [VPC peering connection](https://github.com/ehime/paper-vpcpeering) is created to enable this. In addition to communication between VPCs, most organizations typically also have a requirement for hybrid connectivity, utilizing VPNs or AWS [Direct Connect](https://docs.aws.amazon.com/directconnect/latest/UserGuide/Welcome.html) to connect VPCs to On-Premise networks. At a small scale, involving only a few VPCs, connectivity is _manageable_ at best. Consider the following example, with _5 VPCs_ that we would like to connect via peering in addition to On-Premise via VPN:

![VPC Peering Flow Diagram](assets/vpc-peering.png)

<sup><center><b>Image 1:</b> Counting the number of connections required to connect VPCs to each other and On-Premise</center></sup>
