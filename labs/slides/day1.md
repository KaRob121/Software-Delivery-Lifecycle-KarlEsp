# Day 1 – Environment Lifecycle

Today's session covers the full environment lifecycle, including how software moves through development, test, and production stages and how teams manage data and test cycles to ship safely and repeatably.

- Development, test, and production stages
- Environment refresh cycles
- Test Data Management
- Supporting weekly test cycles

---

## What is the Software Development Lifecycle?

The Software Development Lifecycle (SDLC) describes how software moves from an initial idea through development, testing, deployment, and ongoing production support. Every organisation follows some version of it, even if they don't call it by that name.

The SDLC gives teams a shared language and a controlled process for delivering changes. Without it, teams deploy untested code, skip reviews, and discover problems in production.

---

## ITIL v4 and IT Services

ITIL v4 (Information Technology Infrastructure Library) is a framework for managing IT services across their full lifecycle. It provides common terminology and best practices used across enterprise IT.

Under ITIL, IT systems are treated as **services** that deliver value to customers. All services a team manages are organised into a **service portfolio**. The goal of every change is to improve or protect that value.

---

## SDLC Stages

Software moves through structured stages from idea to production. Each stage has a defined purpose and set of outcomes.

- **Plan:** define requirements, scope, and business value
- **Develop:** build the feature or fix in a controlled branch
- **Test:** validate behaviour in a staging environment before release
- **Deploy:** promote the tested version to production
- **Operate:** monitor, support, and maintain the running service

---

## Delivery Roles

Different roles own different phases of the SDLC. Understanding who is responsible for what prevents duplication and gaps.

| Role | Focus |
|------|-------|
| Product Owner | What should we build next? |
| Business Analyst | What problem are we solving? |
| Project Manager | Are we on time and in scope? |
| Developer | Build it. |
| Ops / SRE | Keep it running. |

---

## What is a Staging Environment?

A staging environment is an isolated copy of the production system used to test and validate changes before they affect customers. It runs the same application code, the same configuration, and ideally the same infrastructure shape as production.

The key word is **isolated**. A bug in staging does not break production. An experiment in dev has no effect on QA. Each environment is independent.

---

## Why Staging Environments Exist

Shipping untested code directly to production is a well-understood risk. Staging environments create a safety net between development and customers, and changes are validated at each stage before being promoted to the next.

Staging also allows different stakeholders to interact with the software before it goes live. QA teams test it, product owners review it, and security teams can audit it, all without touching production.

---

## The Three-Stage Strategy

The most common staging model uses three environments: **dev**, **QA**, and **prod**. Code always promotes left to right and never skips a stage.

- **Dev:** where active development happens, may be unstable
- **QA:** stable enough for structured testing, mirrors production closely
- **Prod:** customer-facing, only receives code that passed QA

---

## Version Control

A Version Control System (VCS) is a centralised store for code that tracks every change ever made. Bitbucket, GitHub, and GitLab are all VCS platforms built on Git.

Version control gives teams:
- A single authoritative copy of the codebase
- Full history of who changed what and why
- Controlled promotion of code between environments
- Tags that mark specific commits for release

---

## Semantic Versioning

Releases are labelled using a standard format: **MAJOR.MINOR.PATCH**. The numbers communicate the nature of the change, not just a sequence.

| Segment | When to increment |
|---------|-------------------|
| MAJOR | Breaking change, existing callers must update |
| MINOR | New feature, backwards compatible |
| PATCH | Bug fix, no API change |

---

## Stage Suffixes for Internal Releases

For internal software, teams append a stage suffix to communicate which environment a build targets.

- `v1.1.0-dev`, built from dev, deployed to the development environment
- `v1.1.0-qa`, promoted to QA for structured testing
- `v1.1.0-prod`, approved for production

Public or LTS software uses plain tags like `v1.0.0`. External users don't care which internal stage it came from.

---

## Release Management

Releasing software to production is a controlled event, not a casual file copy. A good release procedure reduces risk and gives the team a recovery path if something goes wrong.

A release should include:
- **Release strategy:** how the update is applied (blue/green, canary, rolling, recreate)
- **Downtime notification:** informing stakeholders of expected impact
- **Rollback plan:** how to revert quickly if the release fails

---

## Change Advisory Board

Enterprise teams use a CAB (Change Advisory Board) to approve changes before they reach production. The CAB is a meeting where stakeholders review the change, understand the risk, and allocate support resources.

CAB approval is typically required for significant changes and is mandatory during regulated periods. It adds a human checkpoint between QA approval and production deployment.

---

## Rollback and Disaster Recovery

No release process is complete without a plan for when things go wrong. A rollback plan defines how to revert to the previous version quickly. A disaster recovery plan covers what to do if rollback also fails.

- **Rollback:** redeploy the last known good version
- **Disaster recovery:** restore from backup, fail over to secondary region
- **Post-release checks:** monitoring and validation after go-live to catch issues before users report them

---

## The Pull Request Workflow

No code reaches `main` without going through a Pull Request. Developers work on feature branches, open a PR when the work is ready, and a reviewer approves it before it merges.

This controlled handoff is the foundation of a safe delivery workflow. It prevents untested or unreviewed code from reaching the branch that reflects production.

---

## Branching Strategy

A simple branching strategy keeps the delivery pipeline clean. `main` always reflects production-ready code. All active development happens on short-lived branches created from `main`.

- Create a branch for each piece of work
- Open a PR when the work is ready for review
- Merge to `main` only after approval
- Delete the branch after merge to keep the repository clean

---

## What does incrementing MAJOR mean in semantic versioning?

- A) A new feature was added that is backwards compatible
- B) A bug was fixed with no change to the API
- C) A breaking change was introduced that requires callers to update
- D) The version was released to a production environment

---

## What does incrementing MAJOR mean in semantic versioning?

- A) A new feature was added that is backwards compatible
- B) A bug was fixed with no change to the API
- **C) A breaking change was introduced that requires callers to update**
- D) The version was released to a production environment

---

## What is the purpose of a Pull Request?

- A) To deploy code directly to the production branch
- B) To create a new branch from an existing one
- C) To request a merge of two remote repositories
- D) To propose changes for review before they are merged into the target branch

---

## What is the purpose of a Pull Request?

- A) To deploy code directly to the production branch
- B) To create a new branch from an existing one
- C) To request a merge of two remote repositories
- **D) To propose changes for review before they are merged into the target branch**

---

## Which role is responsible for managing the service backlog and prioritising what gets built?

- A) Business Analyst
- B) Project Manager
- C) Product Owner
- D) DevOps Engineer

---

## Which role is responsible for managing the service backlog and prioritising what gets built?

- A) Business Analyst
- B) Project Manager
- **C) Product Owner**
- D) DevOps Engineer

---

## Which version tag would you apply to a release deployed to QA in an internal project?

- A) `v1.1.0`
- B) `v1.1.0-dev`
- C) `v1.1.0-qa`
- D) `v1.1.0-rc`

---

## Which version tag would you apply to a release deployed to QA in an internal project?

- A) `v1.1.0`
- B) `v1.1.0-dev`
- **C) `v1.1.0-qa`**
- D) `v1.1.0-rc`

---

## What should the `main` branch always represent?

- A) The latest code under active development
- B) Production-ready code that has been reviewed and approved
- C) The most recent commit from any team member
- D) A backup copy of the repository

---

## What should the `main` branch always represent?

- A) The latest code under active development
- **B) Production-ready code that has been reviewed and approved**
- C) The most recent commit from any team member
- D) A backup copy of the repository

---

# Lab 1.1

---

## Infrastructure as Code

Infrastructure as Code (IaC) means defining cloud resources in configuration files rather than clicking through a web console. The files are versioned, reviewed, and applied automatically, the same way application code is deployed.

Terraform is the most widely used IaC tool. You describe the desired state of your infrastructure and Terraform calculates what needs to be created, updated, or destroyed to reach that state.

---

## What Terraform Provisions in This Lab

The `terraform/main.tf` file in the deployment repository defines everything needed to run the Order Match API on AWS.

- An **ECS cluster** to run containers
- An **IAM execution role** that allows ECS to pull images and write logs
- A **security group** that opens port 8000 to inbound traffic
- **CloudWatch log groups** for each environment
- **ECS task definitions** and **services** for dev and prod

---

## AWS ECS Fargate

Amazon ECS (Elastic Container Service) with the Fargate launch type runs containers without requiring you to manage servers. You define the container image, CPU, memory, and network settings. AWS handles the underlying compute.

Fargate tasks receive a public IP address directly. No load balancer is required for this lab. Traffic reaches the container on port 8000 using the task's public IP.

---

## Container Images and Docker Hub

A container image is a packaged, runnable version of the application. The Order Match API images are published to Docker Hub under `innovationinsoftware/order-match-api`.

Each image is tagged with a version number: `v1.0.0`, `v1.0.1`, `v1.1.0`, and so on. The deployment pipeline takes a tag as input and tells ECS which version to run.

---

## What a Deployment Pipeline Does

A deployment pipeline automates the steps needed to move a new version of software into an environment. It removes the risk of manual errors and creates a repeatable, auditable record of every deployment.

In this lab the pipeline takes a version tag as input, registers a new ECS task definition pointing to that image version, and updates the ECS service to run it.

---

## Self-Service vs. Auto-Trigger Pipelines

Auto-trigger pipelines run automatically on every push to a branch. This is fast but can flood environments with unreviewed changes.

A self-service pipeline runs on demand. The operator chooses the version to deploy and the target environment, then triggers the pipeline manually. This gives teams precise control over what reaches each stage and when.

---

## Pipeline Repository Variables

Pipelines need credentials and configuration that cannot be stored in source code. Bitbucket repository variables store these values securely and inject them into the pipeline at runtime.

For this lab the required variables are:
- `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`, IAM credentials
- `AWS_ACCOUNT_ID` and `AWS_DEFAULT_REGION`, AWS account context
- `DOCKERHUB_IMAGE`, the image name on Docker Hub

---

## Deploying a Specific Version to a Specific Environment

The `deploy-dev` and `deploy-prod` pipelines each accept a `TAG` input. The pipeline substitutes that tag into the task definition and updates the corresponding ECS service.

The same pipeline code deploys any version to the correct environment. The operator controls both: which version and which target.

---

## Why Environments Run Different Versions Simultaneously

Dev and prod intentionally run different versions at the same time. Prod is on the last stable release. Dev is running the newest change. This is intentional and reflects how far each version has been validated.

Code promotes left to right. When dev is validated, it promotes to QA. When QA passes, it promotes to prod.

---

## `deploy-dev` vs. `deploy-prod`

Both pipelines follow the same steps but target different ECS services. `deploy-dev` updates `order-match-api-dev`. `deploy-prod` updates `order-match-api-prod`.

The separation prevents accidental production deployments. Deploying to dev requires no special approval. Deploying to prod is a deliberate, separate action.

---

## What `terraform-apply` Creates

Running `terraform-apply` reads `terraform/main.tf` and provisions all resources that don't yet exist. Terraform calculates a plan first, so you see what will be created before anything changes.

Resources are only created once. Subsequent runs update resources where the config has changed. Terraform tracks state so it knows what already exists.

---

## `terraform-destroy` and Cleanup

`terraform-destroy` removes every resource Terraform created. ECS Fargate charges by the second, and a running task left overnight will accumulate cost.

Always run `terraform-destroy` when you are done with a lab. A destroy pipeline step is provided in the repository for exactly this purpose.

---

## Adding a New Environment

Dev and prod follow an identical structure in three files. Adding QA means repeating that structure with `qa` substituted throughout.

- `task-definitions/qa.json`, a copy of `dev.json` with QA family and log group names
- `bitbucket-pipelines.yml`, a `deploy-qa` step following the same pattern as `deploy-dev`
- `terraform/main.tf`, QA log group, task definition, and ECS service blocks

---

## Verifying a Deployment

After a pipeline run completes, confirm the deployment worked by checking the running service.

Navigate to **ECS → Clusters → order-match-api → Services → [service] → Tasks**. Click the running task. Copy the **Public IP**. Open a browser and visit `http://<public-ip>:8000/orders`. A JSON response confirms the service is running.

---

## Environment Verification

Before moving to the next lab, confirm all three environments are running the expected versions and responding.

| Environment | Version | Endpoint |
|-------------|---------|----------|
| prod | `v1.0.0` | `http://<prod-ip>:8000/orders` |
| dev | `v1.0.1` | `http://<dev-ip>:8000/orders` |
| QA | `v1.0.1` | `http://<qa-ip>:8000/orders` |

---

## What makes a deployment pipeline "self-service"?

- A) It deploys automatically whenever code is pushed to a branch
- B) It runs on a schedule at a fixed time each day
- C) It runs on demand, with the operator choosing the version and environment
- D) It deploys to all environments simultaneously

---

## What makes a deployment pipeline "self-service"?

- A) It deploys automatically whenever code is pushed to a branch
- B) It runs on a schedule at a fixed time each day
- **C) It runs on demand, with the operator choosing the version and environment**
- D) It deploys to all environments simultaneously

---

## Which AWS service runs containers without requiring you to manage servers?

- A) AWS Lambda
- B) Amazon EC2
- C) AWS Batch
- D) Amazon ECS Fargate

---

## Which AWS service runs containers without requiring you to manage servers?

- A) AWS Lambda
- B) Amazon EC2
- C) AWS Batch
- **D) Amazon ECS Fargate**

---

## Why do dev and prod intentionally run different versions at the same time?

- A) Because the deployment pipeline runs in parallel to both environments
- B) To reduce infrastructure cost by staggering deployments
- C) Because dev validates new changes before they are promoted to prod
- D) Because prod is always ahead of dev in the release cycle

---

## Why do dev and prod intentionally run different versions at the same time?

- A) Because the deployment pipeline runs in parallel to both environments
- B) To reduce infrastructure cost by staggering deployments
- **C) Because dev validates new changes before they are promoted to prod**
- D) Because prod is always ahead of dev in the release cycle

---

## What does `terraform-apply` do in the deployment repository?

- A) Deploys a new container image to an existing ECS service
- B) Destroys all AWS resources created for the lab
- C) Runs the regression test suite against the infrastructure
- D) Provisions the ECS cluster, services, IAM role, and log groups

---

## What does `terraform-apply` do in the deployment repository?

- A) Deploys a new container image to an existing ECS service
- B) Destroys all AWS resources created for the lab
- C) Runs the regression test suite against the infrastructure
- **D) Provisions the ECS cluster, services, IAM role, and log groups**

---

## Where in the AWS Console do you find a running ECS task's public IP address?

- A) ECS → Task Definitions → [definition]
- B) EC2 → Instances → [instance]
- C) ECS → Clusters → [cluster] → Services → [service] → Tasks → [task]
- D) VPC → Subnets → [subnet] → Available IP addresses

---

## Where in the AWS Console do you find a running ECS task's public IP address?

- A) ECS → Task Definitions → [definition]
- B) EC2 → Instances → [instance]
- **C) ECS → Clusters → [cluster] → Services → [service] → Tasks → [task]**
- D) VPC → Subnets → [subnet] → Available IP addresses

---

# Lab 1.2

---

## What is Test Data Management?

Test Data Management (TDM) is the practice of ensuring that test environments have appropriate, controlled, and realistic data. Without it, teams test against empty environments, stale records, or real customer data.

Good TDM defines how data is created, refreshed, and governed across every non-production environment.

---

## Why Test Environments Need Realistic Data

A test environment that mirrors production structure but contains no data produces misleading results. The application code is never exercised under realistic load, realistic data volumes, or realistic edge cases.

An order matching system with zero orders will pass every test written for it. The tests confirm the system handles nothing, not that it handles production conditions correctly.

---

## The Risk of an Empty Test Environment

Testing against an empty environment creates false confidence. Every test passes because there is nothing to break. Edge cases involving existing records, duplicate IDs, or conflicting states are never exercised.

When that version reaches production, it encounters conditions it was never tested against, because real data now exists.

---

## Why Production Data Cannot Be Used in Test Environments

The simplest solution, copying production data into test, is not allowed. Production data contains real customer information. Moving it to a less-controlled environment creates compliance and legal risk that far outweighs the convenience.

This is not a preference. It is a regulatory requirement in most industries.

---

## What is PII?

Personally Identifiable Information (PII) is any data that can be used to identify a specific individual. In a financial or e-commerce system this includes customer names, email addresses, order history, payment details, and account IDs.

Even internal systems that never hold consumer data often hold employee records that are equally regulated. If a test environment contains PII, it carries the same security requirements as production.

---

## GDPR and HIPAA

GDPR (General Data Protection Regulation) applies to any organisation handling personal data of EU residents. HIPAA (Health Insurance Portability and Accountability Act) applies to US healthcare data.

Both regulations restrict where personal data can be stored, who can access it, and what happens when it is breached. Neither regulation makes exceptions for development or QA environments.

---

## A Breach in Dev Has the Same Consequences as a Breach in Prod

Organisations sometimes treat dev environments as low-risk because they are not customer-facing. The regulations disagree.

If a dev environment containing real customer data is breached, the organisation faces the same notification obligations, potential fines, and reputational damage as a production breach. The environment's purpose does not change the classification of the data it holds.

---

## What is Synthetic Data?

Synthetic data is generated rather than collected. It has the same structural characteristics as real data, including the same fields, data types, and realistic value ranges, but contains no real information about any individual.

A synthetic order history contains realistic prices, quantities, and timestamps. None of it corresponds to a real customer or a real transaction.

---

## Synthetic vs. Anonymised Data

Anonymised data is real production data with identifying fields removed or replaced. Synthetic data was never real. The distinction matters because anonymisation is reversible, and sophisticated attacks can re-identify individuals from seemingly anonymised datasets.

Synthetic data eliminates this risk entirely. There is no real person behind the data, so there is nothing to re-identify.

---

## Generating Synthetic Data for the Order Match API

The Order Match API accepts orders with three fields: `side` (buy or sell), `price` (a float), and `quantity` (an integer). Generating synthetic orders means selecting realistic random values for each field across a set of POST requests.

Python's `random` module handles this without any external dependencies. The result is a dataset that resembles production usage without containing any real trades.

---

## Properties of Good Synthetic Data

Synthetic data should reflect the distribution and variation of real data, not just fill fields with defaults.

- **Realistic ranges:** prices between $50 and $200, not always $1.00
- **Variety:** a mix of buy and sell orders, not all one side
- **Volume:** enough records to exercise edge cases and sorting logic
- **Repeatability:** the same script produces a fresh, valid dataset every time

---

## What is an Environment Refresh Cycle?

A refresh cycle is a scheduled process that resets a test environment to a known baseline state. The environment is seeded with a fresh synthetic dataset, replacing whatever accumulated during the previous cycle.

Weekly is the most common cadence. At the start of each test week the team knows exactly what state each environment is in, which makes test results easier to interpret and compare.

---

## Why Environments Go Stale

Every test run adds data to an environment. Over time, orders created during testing, failed transactions, and cancelled records accumulate. None of this was planned. It is the residue of previous activity.

Stale data creates noise. Tests fail for reasons unrelated to the code under test. Results are hard to compare across runs because the starting state is different each time.

---

## The Weekly Refresh Cadence

Running the seed step at the start of each test week ensures every cycle begins from the same baseline. Teams can compare this week's test results directly against last week's because the data setup was identical.

The cadence does not have to be weekly. Some teams refresh daily, others monthly. What matters is that the refresh is scheduled, documented, and repeatable.

---

## Seeding as a Pipeline Step

A seeding script that runs manually is better than nothing. A seeding script that runs as a pipeline step is better still, as it is triggered consistently, produces a log, and can be run by anyone on the team without a local environment setup.

The `seed-dev` pipeline is triggered manually with the environment's `BASE_URL` as input. Running it takes under a minute and produces 20 fresh synthetic orders.

---

## Why can production data not be copied into test environments?

- A) Production data is too large to copy efficiently
- B) Test environments run a different version of the application
- C) It contains PII, and its use outside production may violate GDPR or HIPAA
- D) Production databases use a different schema than test databases

---

## Why can production data not be copied into test environments?

- A) Production data is too large to copy efficiently
- B) Test environments run a different version of the application
- **C) It contains PII, and its use outside production may violate GDPR or HIPAA**
- D) Production databases use a different schema than test databases

---

## What best describes synthetic test data?

- A) A copy of production data with customer names removed
- B) Data manually entered by QA engineers during test runs
- C) Real transaction data exported from a staging environment
- D) Generated data with realistic structure and distribution but no real customer information

---

## What best describes synthetic test data?

- A) A copy of production data with customer names removed
- B) Data manually entered by QA engineers during test runs
- C) Real transaction data exported from a staging environment
- **D) Generated data with realistic structure and distribution but no real customer information**

---

## What is an environment refresh cycle?

- A) Restarting the ECS service to pick up a new container image
- B) Replacing AWS infrastructure by running terraform-destroy then terraform-apply
- C) A scheduled reseed that replaces stale test data with a fresh synthetic dataset
- D) Updating Bitbucket pipeline variables with new environment credentials

---

## What is an environment refresh cycle?

- A) Restarting the ECS service to pick up a new container image
- B) Replacing AWS infrastructure by running terraform-destroy then terraform-apply
- **C) A scheduled reseed that replaces stale test data with a fresh synthetic dataset**
- D) Updating Bitbucket pipeline variables with new environment credentials

---

## What problem does stale test data cause over time?

- A) It causes the ECS task to run out of memory
- B) It prevents the Terraform state from being updated correctly
- C) It makes Docker Hub images inaccessible
- D) Accumulated old records make test results harder to interpret and less reliable

---

## What problem does stale test data cause over time?

- A) It causes the ECS task to run out of memory
- B) It prevents the Terraform state from being updated correctly
- C) It makes Docker Hub images inaccessible
- **D) Accumulated old records make test results harder to interpret and less reliable**

---

## Which Python library does the seeding script use to post orders to the API?

- A) `urllib`
- B) `httpx`
- C) `requests`
- D) `boto3`

---

## Which Python library does the seeding script use to post orders to the API?

- A) `urllib`
- B) `httpx`
- **C) `requests`**
- D) `boto3`

---

# Lab 1.3

---

## What is a Test Cycle?

A test cycle is a structured, repeatable sequence of activities that validates a software environment before it is promoted to the next stage. The cycle has a defined starting state, a set of activities, and a documented outcome.

Without a defined cycle, testing is ad hoc. Some things get checked, others are forgotten, and results from one week cannot be compared to the next.

---

## The Weekly Test Cycle

Teams that ship on a regular cadence often run a weekly test cycle. Each week begins with a known state and ends with a recorded outcome.

The four phases:
1. **Seed:** reset the environment with fresh synthetic data
2. **Deploy:** promote the target version to the environment
3. **Test:** run the regression suite against the deployed version
4. **Review:** inspect results, log failures, decide whether to promote

---

## Seed, Deploy, Test, Review

Each phase maps directly to a pipeline step already in the repository.

| Phase | Pipeline step |
|-------|---------------|
| Seed | `seed-dev` |
| Deploy | `deploy-dev` |
| Test | `test-dev` |
| Review | Tests tab in Bitbucket |

Running these steps in sequence is the test cycle. The pipeline is the process.

---

## What is a Regression?

A regression is when a change to one part of the system breaks something that previously worked. It is one of the most common failures in active development. A new feature subtly changes shared state, a dependency upgrade alters default behaviour, a refactor introduces an error in an adjacent function.

Regressions are easy to miss because the team is focused on what changed, not on what was already working.

---

## Why Regressions Happen

No developer intentionally introduces a regression. They happen because software is interconnected and changes have side effects that are not always visible during development.

Common causes:
- A new endpoint reuses a shared function and inadvertently changes its behaviour
- A dependency is upgraded and the new version has different defaults
- A config change affects multiple services at once
- A code path that was working is modified and not retested

---

## The Cost of Catching Regressions in Production

A regression found in the pipeline costs one pipeline run. A regression found in production costs a customer-facing incident, a rollback, a post-mortem, and potentially regulatory reporting.

The earlier in the delivery pipeline a regression is caught, the cheaper it is to fix. This is the primary justification for automated regression testing at every stage.

---

## Tests as Code

Test files live in the same repository as the deployment configuration. They are versioned, reviewed, and updated alongside the code they validate. When a new endpoint is added, a test for it is added in the same commit.

This means test coverage is tracked like any other change. A PR that removes a test is as visible and reviewable as a PR that removes a feature.

---

## pytest

pytest is a Python testing framework used widely in DevOps and backend engineering. Tests are plain Python functions with names that start with `test_`. There is no boilerplate. Write a function, make an assertion, done.

Running `pytest tests/ -v` discovers all test files, executes them, and prints a result for each one. The exit code is non-zero if any test fails, which causes the pipeline step to fail.

---

## Writing Test Assertions

A test assertion is a statement that something must be true. If it is not true, the test fails.

```python
def test_get_orders():
    r = requests.get(f"{BASE_URL}/orders")
    assert r.status_code == 200
    assert isinstance(r.json(), list)
```

This test checks two things: the endpoint returns a 200 status code and the response body is a JSON list. If either assertion fails, pytest reports the test as failed.

---

## Round-Trip Tests

A round-trip test creates a record and then retrieves it. This validates both the write path and the read path in a single test, and confirms the API returns consistent data.

```python
def test_get_order_by_id():
    r = requests.post(f"{BASE_URL}/orders", json=body)
    order_id = r.json()["id"]
    r2 = requests.get(f"{BASE_URL}/orders/{order_id}")
    assert r2.json()["id"] == order_id
```

---

## Negative Tests

A negative test confirms that the system handles invalid input or missing records correctly. The most common API negative test is verifying that a 404 is returned for a non-existent resource.

```python
def test_order_not_found():
    r = requests.get(f"{BASE_URL}/orders/999999")
    assert r.status_code == 404
```

Without negative tests, a test suite only confirms that the happy path works.

---

## Running Tests Against a Deployed Environment

Tests read the target environment's URL from the `BASE_URL` environment variable. The same test file runs against dev, QA, or prod. Only the variable changes.

In the pipeline, `BASE_URL` is passed as a required input variable when the pipeline is triggered. Locally it is set before running pytest:

```
BASE_URL=http://<dev-ip>:8000 pytest tests/ -v
```

---

## JUnit XML

JUnit XML is a standard format for recording test results. It was created for the Java ecosystem but is now supported by virtually every CI/CD platform, including Bitbucket Pipelines.

pytest generates JUnit XML with one flag: `--junitxml=test-results/results.xml`. The output file contains one entry per test: name, duration, and pass/fail status. The pipeline step declares this file as a report artifact.

---

## Bitbucket's Tests Tab

When a pipeline step declares a JUnit XML file as an artifact, Bitbucket parses it and renders a **Tests** tab on the pipeline run. The tab shows:

- Total test count and pass/fail breakdown
- Each individual test name and its result
- Duration for each test
- The full error message for any failure

The report is captured even if the pipeline step fails, so you can always inspect which tests failed.

---

## Test History and Trend Tracking

Every time a `test-dev` pipeline runs, its results are added to the history. Over time you can see exactly when a test started failing and correlate it with the deployment that caused the regression.

This history turns individual pipeline runs into a trend. A test suite that has passed for six consecutive weeks and then fails on the seventh is a clear signal that something in last week's deployment broke something.

---

## What is a regression in software delivery?

- A) A deliberate rollback to a previous version of the application
- B) A new change that breaks behavior that previously worked
- C) A test that was written incorrectly and produces false results
- D) A deployment that fails to complete successfully

---

## What is a regression in software delivery?

- A) A deliberate rollback to a previous version of the application
- **B) A new change that breaks behavior that previously worked**
- C) A test that was written incorrectly and produces false results
- D) A deployment that fails to complete successfully

---

## What does the `--junitxml` flag do when running pytest?

- A) Runs only the tests that previously failed
- B) Generates a visual HTML report of test results
- C) Uploads results directly to Bitbucket
- D) Writes test results to an XML file in the JUnit format

---

## What does the `--junitxml` flag do when running pytest?

- A) Runs only the tests that previously failed
- B) Generates a visual HTML report of test results
- C) Uploads results directly to Bitbucket
- **D) Writes test results to an XML file in the JUnit format**

---

## What Bitbucket feature renders test results from a pipeline run?

- A) The Artifacts panel in the pipeline logs
- B) The Insights dashboard in the repository overview
- C) The Tests tab, populated from the JUnit artifact declared in the pipeline step
- D) The Diff view in the pull request comparison

---

## What Bitbucket feature renders test results from a pipeline run?

- A) The Artifacts panel in the pipeline logs
- B) The Insights dashboard in the repository overview
- **C) The Tests tab, populated from the JUnit artifact declared in the pipeline step**
- D) The Diff view in the pull request comparison

---

## What is the correct order of phases in a weekly test cycle?

- A) Deploy, Seed, Review, Test
- B) Test, Deploy, Seed, Review
- C) Review, Test, Seed, Deploy
- D) Seed, Deploy, Test, Review

---

## What is the correct order of phases in a weekly test cycle?

- A) Deploy, Seed, Review, Test
- B) Test, Deploy, Seed, Review
- C) Review, Test, Seed, Deploy
- **D) Seed, Deploy, Test, Review**

---

## What HTTP status code does a successful `POST /orders` return?

- A) 200 OK
- B) 201 Created
- C) 202 Accepted
- D) 204 No Content

---

## What HTTP status code does a successful `POST /orders` return?

- A) 200 OK
- **B) 201 Created**
- C) 202 Accepted
- D) 204 No Content

---

# Lab 1.4
