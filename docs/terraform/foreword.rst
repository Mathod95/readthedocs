Foreword
++++++++

What is Infrastructure as Code ?
================================

Infrastructure as Code (IaC)
You write a configuration script to automate creating, updating or destroying cloud infrastructure.
- IaC is a blueprint of your infrastructure
- IaC allows you to easily share, version or inventory your cloud infrastructure

Manual configuration
Manually configuring your cloud infrastructure allows you easily start using new service offerings to quickly prototype architectures however it comees with many downsides:
- It's easy to mis-configure a service though human error
- It's hard to manage the expected state of configuration for compliance
- It's hard to transfer configuration knowledge to other team members

Declarative / Imperative
========================

Declarative
-----------
- What you see is what you get. Explicit
- More verbose, but zero chance of misconfiguration
- Use scripting languages (json, yaml, xml, ...)

Exemple of tool
- Azure Blueprints - Azure
- CloudFormation - AWS
- Cloud Deployment Manager - GCP
- Terraform - Support AWS, Azure, GCP, K8s

Imperative
----------
- You say what you want, and the rest is filled in. Implicit
- Less verbose, you could end up with misconfiguration
- Does more than Declarative
- Use programming languages (Python, Ruby, Javascript, ...)

Exemple of tool
- AWS Cloud Development Kit - AWS
- Pulumi - Support AWS, Azure, GCP, K8s


What is a container ?
---------------------
Containers before Docker
------------------------
Why use containers?
-------------------
Problems introduced with containers
-----------------------------------
What will Kubernetes be used for?
---------------------------------
External resources
------------------

A word about the application
============================

There is no point in running
----------------------------
The twelve application factors
------------------------------
Microservices vs. Monoliths
---------------------------