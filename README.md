<div>
  <p align="center">
    <img width=60% src="images/gsoc.svg"> <img width=35% src="images/cncf.svg">
  </p>
</div>

# GSoC 2022 Final Report

**Organization**: CNCF

**Project**: [Tooling to deploy and cross-configure cert-manager with external dependencies by Terraform](https://summerofcode.withgoogle.com/programs/2022/projects/DaL4hA2U)

**Proposal**: https://docs.google.com/document/d/14oJux-d-91Do3DLi5eRG-wUEE4R3Hh7D4u0Yfje3auw/edit?usp=sharing

**Issue**: https://github.com/cert-manager/cert-manager/issues/4855

**Code**: https://github.com/cert-manager/testing-addons

## Introduction
<div>
  <p align="center">
    <img width=25% src="images/cert-manager.svg">
  </p>
</div>

This is my first trip to GSoC and I am honored to be selected by CNCF organization and gradually complete this project in three months. 

Firstly, I am very grateful to my mentor [Irbe Krumina](https://github.com/irbekrm), who gave me great help and patient guidance from the discussion of the scheme to the writing of the proposal, to the development of the project. And thanks to the [Cert-Manager Team](https://github.com/orgs/cert-manager/people), I felt the friendliness and professionalism of the team members in the process of participating in the [daily stand-up meeting](https://cert-manager.io/docs/contributing/#meetings), and it was a wonderful experience to work with you.

I built tooling to help cert-manager maintainers to deploy cert-manager together with some its dependencies and built a framework that will allow maintainers and community to add Terraform modules to deploy other dependencies. We think this will significantly save time for cert-manager developers when testing with external dependencies locally.

## Work Done

### Discuss the scheme and write a formal proposal

I actively participated in the design phase of the project, actively discussed with the mentor under [this issue](https://github.com/cert-manager/cert-manager/issues/4855), compared the advantages and disadvantages of CLI, Script and Terraform modules, and finally chose to use Terraform to design and develop this project, and completed the [final proposal](https://docs.google.com/document/d/14oJux-d-91Do3DLi5eRG-wUEE4R3Hh7D4u0Yfje3auw/edit?usp=sharing).

### Initialize the project and add cert-manager and vault workflow

Firstly, the mentor created a new code repository called [testing-addons](https://github.com/cert-manager/testing-addons) and released the task in the form of an issue, where we discussed some technical details.

I improved this repository as PRs, including adding Readme and adding linter scripts to the CI process, and implemented the deployment and configuration of Cert-manager and Vault workloads using tools such as [Terraform](https://www.terraform.io/downloads), [Terragrunt](https://terragrunt.gruntwork.io/docs/getting-started/install/) and [Helm](https://helm.sh/docs/intro/install/). It divide the entire workflow into `cm-install`, `vault-install`, `cm-config` and `vault-config` Terraform modules, the Terragrunt workflow is responsible for organizing them.

List of PRs to finish these works:

- https://github.com/cert-manager/testing-addons/pull/5
- https://github.com/cert-manager/testing-addons/pull/6
- https://github.com/cert-manager/testing-addons/pull/11
- https://github.com/cert-manager/testing-addons/pull/12
- https://github.com/cert-manager/testing-addons/pull/13
- https://github.com/cert-manager/testing-addons/pull/14
- https://github.com/cert-manager/testing-addons/pull/19
- https://github.com/cert-manager/testing-addons/pull/20
- https://github.com/cert-manager/testing-addons/pull/21
- https://github.com/cert-manager/testing-addons/pull/22
- https://github.com/cert-manager/testing-addons/pull/26
- https://github.com/cert-manager/testing-addons/pull/27
- https://github.com/cert-manager/testing-addons/pull/29
- https://github.com/cert-manager/testing-addons/pull/30
- https://github.com/cert-manager/testing-addons/pull/32
- https://github.com/cert-manager/testing-addons/pull/34

### Add Gateway and Ingress workflows

Since the structure design of the project has been completed in the previous stage, adding a new workflow only needs to divide Terraform modules according to functions, and the project expansion is more convenient.

Adding the Gateway and Ingress workflows is generally smooth, but testing [ACME](https://cert-manager.io/docs/configuration/acme/) requires public cloud services, and I am very grateful to my mentor for helping to test this feature.

List of PRs to finish these works:

- https://github.com/cert-manager/testing-addons/pull/31
- https://github.com/cert-manager/testing-addons/pull/36
- https://github.com/cert-manager/testing-addons/pull/37
- https://github.com/cert-manager/testing-addons/pull/40

## Future Work

Since a relatively complete workflow template is already available, more external dependency test workflows can be easily added later, such as [Prometheus/Grafana workflow](https://github.com/cert-manager/testing-addons/issues/38).

It would be nice to be able to reuse specific Terraform modules to reduce maintenance of duplicate code, but so far there is no better way to [refactor terraform modules to allow sharing cert-manager installation code](https://github.com/cert-manager/testing-addons/issues/23). This issue is worth continuing to explore.

It may have been good to add to the Readme [how a developer should add a new workflow](https://github.com/cert-manager/testing-addons/issues/41).

## Conclusion

With this, the project was finally completed. We designed and developed a tool to deploy and cross-configure cert-manager with external dependencies that can reduce the amount of time maintainers spend figuring out how to setup necessary infrastructure for different scenarios in which cert-manager can be used (i.e. to reproduce user reported bugs).

If you want to use the project, you can clone the [testing-addons](https://github.com/cert-manager/testing-addons) repository locally and deploy the workflow that you need.

I also presented my work at the bi-weekly cert-manager [developer meeting](https://cert-manager.io/docs/contributing/#meetings) on [27th July 2022](https://docs.google.com/document/d/1Tc5t6ylY9dhXAan1OjOoldeaoys1Yh4Ir710ATfBa5U/edit#). 

The video recording of the meeting can be found at https://www.youtube.com/watch?v=dub3x5qRTqc&ab_channel=cert-manager.
