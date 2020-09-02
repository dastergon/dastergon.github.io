---
title: "The Production Readiness Spectrum"
description: "An article on how to get started with Production Readiness
Reviews"
date: 2020-09-02T19:45:15+02:00
draft: false
toc: false
images: ["prr-spectrum.png"]
tags:
    - sre
    - site-reliability-engineering
    - devops
    - production-readiness
---
![The Production Readiness Spectrum](/prr-spectrum.png)

How do we define the production-readiness of services? How can we know that a service is ready for prime time?

A "production-ready" service for an early-stage startup might be a service that has monitoring support, alerts, and a few unit tests. In contrast, in a large corporation, it might be a service with an adequate amount of unit and integration tests, documentation, monitoring, alerts, tracing support, and more.

Production Readiness is not something that we can prescribe. It is a spectrum. What makes a service "production-ready" is a moving target. The technology and the requirements of our organization change over time, so it's impossible to ensure a fixed state of production-readiness in our infrastructure all the time.

A common way for measuring the reliability of a running service is through [Service Level Indicators](https://landing.google.com/sre/sre-book/chapters/service-level-objectives/) (SLIs) and the respective [Service Level Objectives](https://landing.google.com/sre/sre-book/chapters/service-level-objectives/) (SLOs). However, to meet its target SLOs, a service first needs to follow the acceptable production practices of our organization.

Let's see how Production Readiness Reviews (PRRs) can help us solidify our production-ready principles and acceptable operational practices in the organization.

## Chasing operational excellence

Knowledge sharing among teams is essential to exchange good practices and avoid duplicate efforts. Also, it makes teams more unified and engaged. However, sometimes knowledge sharing does not happen to a satisfying degree, and teams end up implementing services within their knowledge boundaries.

Also, when SREs or developers are on-call for a service, certain things are assumed during the mitigation and troubleshooting stage. For example,  meaningful metrics, actionable alerts, playbooks, and documentation for rollout and rollback. Consequently, before requesting on-call support, we should ensure that a service follows the good practices for incident response.

So, how can we tackle these issues?

A method used to tackle such issues is known as Production Readiness Reviews (PRRs). We start by documenting production practices, both already known to our organization and new ones that we found online. Then, we use PRRs as a framework to assess the services and track their compliance. Valid candidates for such reviews are any services currently running in our infrastructure and new services that are planned to go into production.

Some of the benefits of Production Readiness Reviews:
- Eliminate tribal knowledge
- Improve consistency of practices across teams
- Pave the way for on-call friendly services
- Act as a learning tool for interns and new hires

## The Checklist
A common way to record production-readiness practices is in the form of a checklist.

Why a checklist?

Humans make mistakes repeatedly, and we need to embrace the fact that mistakes are inevitable. According to Atul Gawande in his book ["The Checklist Manifesto"](https://www.amazon.com/Checklist-Manifesto-How-Things-Right/dp/0312430000), when it comes to making mistakes in the workplace, there are two different kinds: **ignorance** and **ineptitude**. Ignorance is when we lack information to perform a task, and ineptitude is the failure to apply known information consistently and correctly. Checklists are used across many fields to prevent us from falling into these mistakes.

This following table shows a few topics that our checklist could cover:

| Section  | Topics |
|-------|-------|
| General | Description of a service, ownership declaration  |
| Architecture | design docs, diagrams, and tradeoffs discussions|
| Development Process | unit tests, integration tests, version control, external dependencies, build and test pipelines |
| Change Management | Process and rollback techniques, canary deployments|
| Capacity Planning | Load testing, load shedding |
| Observability | Monitoring, dashboards, logging, tracing support|
| Incident Response | Runbooks, alerts, SLIs/SLOs|

> Tip: When authoring the checklist, focus on the forest and not the trees.

We should aim for a concise general-purpose checklist that is not tightly coupled to certain services or programming language. Rather, make it adaptable to our current needs and cases without sacrificing the essence.

The following resources offer recommended items for Production Readiness checklists:
- [The Azure Readiness Checklist](https://azurechecklist.com/)
- [Production Readiness Checklist by Gruntwork](https://gruntwork.io/devops-checklist/)
- [Production Checklist for Web Apps on Kubernetes](https://srcco.de/posts/web-service-on-kubernetes-production-checklist-2019.html)
- [Google Cloud Production Guideline](https://medium.com/google-cloud/production-guideline-9d5d10c8f1e)
- [Internet Scale Services Checklist](https://gist.github.com/acolyer/95ef23802803cb8b4eb5)

## Getting started
Bringing Production Readiness Reviews to an organization is not an easy task and requires buy-in from management to make it official, especially if the organization is large or has slow processes. It is also likely that we will encounter skeptical and resistant colleagues throughout this journey.

Individuals that are not familiar with the SRE concepts or have a long tenure at the company are usually skeptical as they are used to doing things in a certain way. Consequently, we have to explain to them the benefits of Production Readiness Reviews and describe what's in it for them. Therefore, to introduce this process needs patience, persistence, and incremental steps to convince management and the skeptics that it is worth the investment.

### Drafting a proposal
How to propose this new process depends highly on the organization. The proposal usually comes in the form of design documentation, RFC, or something similar.

To make our proposal more solid and data-driven, we could create a draft checklist and conduct trials with our colleagues. During the reviews, it is likely that we will find blind spots in the checklist, missing documentation and alerts, and more. At the end of each trial, we should keep notes on what we have found helpful, what we should improve for the next iteration, and what are our peer's suggestions for further development.

> Rule of Thumb: It's a good practice to initially pick services from different domains and scales for wider exposure to the infrastructure.

Other actions that we could take for a smooth introduction to Production Readiness Reviews are by doing introductory talks and showcasing the results of the trials. We could also host open floor discussions and allow our colleagues to tell their opinion about this topic.

### Reviewing
The reviewing process depends on the time that we can invest and the dynamics of the teams.

![The Production Readiness Review Arrow](/prr-review-arrow.png)

#### 1-sided review
This approach requires one or more SREs to manually evaluate and check whether a service complies with the items in the checklist. Alternatively, the developers of a respective service could do the review in their own time.

This type of review is flexible and saves a significant amount of time, but requires discipline and is prone to bias. Developers want to release new features, and SREs want to bring a balance between release velocity and infrastructure stability. Thus, depending on who is evaluating a service, there is a possibility that we will have different results.

#### Group review
This type of review requires two or more people, from different teams, for instance, product developers and SREs, reviewing the service in the same session.

This review reduces bias because, during the session, we hear various opinions from different points of view. However, we should be aware of the conflict of interest between the teams, which needs careful management.

#### Semi-automated reviews
In this review, we have partially automated some compliance checks, but there's still a hands-on review. For example, we could automatically check if the [four golden signals](https://landing.google.com/sre/sre-book/chapters/monitoring-distributed-systems/#xref_monitoring_golden-signals)  of monitoring are tracked for our service.

Semi-automated reviews save a handful of time but require an initial time investment to implement the automated checks. As we progress to an automated solution, we see less conflict of interest and more objective reviews.

#### Automated reviews
In this type of review, we automatically check for compliance for all the topics that we have defined in the Production Readiness checklist. A prominent example is [LinkedIn](https://www.usenix.org/conference/srecon17americas/program/presentation/lawrence) that has implemented an automated scorecard system for production-readiness compliance checks of their services.

Automated reviews save a significant amount of working hours. But, they also rot over time just like any code. Consequently, an initial time investment is required to implement the system, and then, time is needed to maintain it.

### Evaluation and final decision
The evaluation and decision-making approaches can range from strict and proactive to lenient and reactive. In a small-medium business, we might have to deploy a service regardless of the outcome of the review, but we could still keep notes on topics that need further improvements. In a large scale environment, however, we might decide that the service cannot have SRE support, or the deployment cannot proceed without complying with the items in the checklist.

With the Production Readiness Reviews, we can decide how comfortable we feel to roll out a new service to production. However, we can also use [error budgets](https://landing.google.com/sre/sre-book/chapters/embracing-risk/) in conjunction with PRRs to guide us in the decision-making process and balance the risk, in case something slips from the reviews.

#### Licking-the-index finger evaluation
In this evaluation, we go through the checklist in a top-down fashion and check for compliance. Then, we agree if we want to proceed with the release depending on the situation.

This approach is lenient, but it comes with greater risk because it is prone to confirmation bias. However, we can still track what is missing from our service and fix it later.

#### Short-circuit evaluation
In the short-circuit evaluation, we go through the items in the checklist, and when we notice that our service does not meet the requirements, we request further compliance and ask for a follow-up review.

This is a strict and proactive evaluation method but enforces our production-readiness practices.

### Traffic-lights evaluation
In this evaluation, we use the traffic lights (green, yellow, red) analogy.
We classify each category or item with a color or label based on its criticality. Critical items are flagged as critical (red). Items that we should have but are not that critical are flagged as important (yellow), and finally, items that would be great to have but are optional are flagged as green or Suggested.

Failing to comply with the critical items means that a service needs to improve or rework these items before proceeding with another review. In contrast, failing to comply with items flagged as Important means that service gets a green pass, but with warnings, and further tickets should be created. Over time, suggested items should evolve to important ones, otherwise, the teams will not focus on implementing them.

This approach classifies between strict and lenient. Although it is prone to bias, it allows us to balance our PRR topics over time based on how our infrastructure evolves.

#### Score-based evaluation
In the score-based evaluation, we can define numerical points or weights to each category or item on our list based on the criticality. Then, we calculate the final score or grade and decide how to proceed based on our policies.

This approach is more a fine-grained and objective evaluation compared to the rest, but it is the most time consuming and requires critical thinking before associating scores to each category or item.

## Keep the flame burning
It is hard to prevent services from breaking with just a bunch of topics covered in a checklist.  As technology and the organization's scale and requirements change, the production readiness requirements will organically change too. So, the work does not stop once we introduce this new review process. We need to keep the flame burning. Otherwise, the process will stale and eventually fade out.

We need to keep refreshing the checklist, have production readiness discussions, and ask for feedback from our peers through internal surveys. Also, future outages enable us to rethink our production practices and help us enrich the list or cleanup the irrelevant items. Some items in the checklist will become assumptions, and some checks will be automated.  Other things that can help declutter the checklist:
- Cookiecutters and boilerplates for creating new services with the internal best practices
- Portals with design and development guidelines
- Use of policy enforcement software like [Open Policy Agent](https://www.openpolicyagent.org/) for codified compliance checks.
- Monitoring mixins for packaging together templates for dashboards and alerts.

## Closing thoughts
Production readiness is a continuous process. Although not a panacea for production failures and outages, Production Readiness Reviews are a powerful tool that enables us to provide a common language for our production standards across the organization. It increases our confidence throughout the whole lifecycle of a service and builds trust between product development and SRE teams.

Production readiness is a big topic and requires more than one blog posts to discuss it extensively. I hope this article will help you get started and spark discussions within your organization.

## Further Reading
- [The Evolving SRE Engagement Model chapter
 from the Google SRE book](https://landing.google.com/sre/sre-book/chapters/evolving-sre-engagement-model)
- [Production readiness by JBD](https://jbd.dev/prod-readiness/)
- [Are you ready for production? by JBD](https://speakerdeck.com/rakyll/are-you-ready-for-production)
- [How to Improve Your Service by Roasting It](https://www.usenix.org/conference/srecon16europe/program/presentation/welch)
- [Site Reliability Engineering Resources](https://github.com/dastergon/awesome-sre)

