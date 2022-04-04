# W3F Grant Proposal

> This document will be part of the terms and conditions of your agreement and therefore needs to contain all the required information about the project. Don't remove any of the mandatory parts presented in bold letters or as headlines! Lines starting with a `>` (such as this one) can be removed.
>
> See the [Grants Program Process](https://github.com/w3f/Grants-Program/#pencil-process) on how to submit a proposal.

- **Project Name:** Trust Protocol
- **Team Name:** Verifive
- **Payment Address:** BTC, Ethereum (USDT/DAI) or Karura (kUSD) payment address. Please also specify the currency. (e.g. 0x8920... (DAI))
- **[Level](https://github.com/w3f/Grants-Program/tree/master#level_slider-levels):** 2

> ⚠️ *The combination of your GitHub account submitting the application and the payment address above will be your unique identifier during the program. Please keep them safe.*

## Project Overview :page_facing_up:
### Overview

// Groom

Please provide the following:

- If the name of your project is not descriptive, a tag line (one sentence summary).
- A brief description of your project.
- An indication of how your project relates to / integrates into Substrate / Polkadot / Kusama.
- An indication of why your team is interested in creating this project.

----

The internet has been created without a trust or identity protocol. This is probably due to the fact that the main challenge at the time was the connectivity of so many computers. Today we are faced with an issue about trust: how do you decide to trust [energyweb.org](https://hackmd.io/y52lFOTIRUigKH_QACEP5w) over [energyweb.io](https://hackmd.io/y52lFOTIRUigKH_QACEP5w)? Which one is the true Energy Web Foundation?

In the above instance, it’s easy as the former links to a website of the EWF while the latter is parked domain. But what if they both link to a similar website protected by an SSL certificate and claiming to be the genuine EWF? How do you tell them appart?

This is where digital identities or DID come in handy. If both [energyweb.org](https://hackmd.io/y52lFOTIRUigKH_QACEP5w) and [energyweb.io](https://hackmd.io/y52lFOTIRUigKH_QACEP5w) present me with a DID and the former has a claim from the Swiss government that it is a foundation and the latter lacks this credential, then it is easy for me to decide; because I know that the real EWF is a swiss foundation.

[Verifiable Credentials (VC)](https://www.w3.org/TR/vc-data-model/) are signed claims which (minimally) have an `Issuer` a `Subject` and a `Proof` so that when presented, they can be verified by a `Verifier`. There is no mandate to use a blockchain to anchor or store any of the data and it is meant to be self contained and `Complete` upon presentation.

#### Introduction

The basic DID functionality is to associate a key pair with an identity and store this association in a publicly accessible storage. We prefer the decentralised, immutable kind; AKA a blockchain.

![DID Registry](https://res.cloudinary.com/mhrsntrk/image/upload/v1646837908/veri5/1_mxqjum.png)

Once the identities and associated keys have been stored, any DID acting as an `issuer`, can create a `verifiable credential` and send it to a `holder`. In general the holder will ask for the VC first and the issuer will respond to this request by issuing the VC.

![Verifiable Credentials](https://res.cloudinary.com/mhrsntrk/image/upload/v1646837909/veri5/2_dl3bqc.png)

The `holder` can then, at their leisure, create a `verifiable presentation` containing one ore more VCs and send it to an arbitrary DID which will act as the `verifier`. The verifier will access the Ledger to make sure that the keys used for signing the VCs are registered to the correct DIDs. The verifier makes sure everything is `correct`.

![Verification](https://res.cloudinary.com/mhrsntrk/image/upload/v1646837909/veri5/3_m3cqn9.png)

#### The Missing link

What is missing in the DID process is a way to check that the VC was issued by the right party and even more importantly, that processes which require multiple VCs to be issued can be documented and verified in a decentralised manner.

As this is very abstract, an example would be helpful: 

> A supermarket chain, Super Organic Markets (SOM), wants to make sure that all of its organic produce is supplied by organic farmers only.
> 

The process to become a recognised organic farmer has been established as follows:

- Get certified by the Association of Organic Farmers (AOF)
    - This involves having the accounts audited every year by one of the approved auditors
    - The farmers must also pay a membership fee to the association
    - For diary farms, an annual visit by an animal welfare expert is also mandated
- Be registered with the national commerce registry (NCR)
- Have a bank account with one of the SOM’s partner banks (SPBa, SPBb and SPBc)

In order to reduce the administrative overhead, SOM has convinced all the participants to use `the Kilt protocol` to create identities and issue credentials. 

SOM has published the identities of the issuing parties (AOF, NCR and SPB?) on their website to make sure that everyone can verify the Verifiable Credentials of farmers. It also makes available a web-app which helps farmers perform the registration.

##### But complexity looms

This all works well as long as there is only one supermarket chain involved. But after a year of operations, 12 other super market chains in the country find the process helpful and would like to do the same thing. 

As SOM has published the identities of the issuers on its website, in a static HTML, there is no easy way to retrieve the information programatically. On top of that, if some information changes, a manual process is required to perform the update, 12 times. Not only is the latency of change high, but the probability of someone making a mistake is even higher.

Also, because the data is published in an HTML file, there is no versioning or historic data. It is not possible to check if a VC was valid 12 months ago if it is not valid today. Unless of course the verifier has stored the history in their own system.

Also, everyone just blindly trusts the AOF to do its work properly and apply the same rules to all its members. There are many example internationally of such associations breaking their own rules. This is why the AOF has chosen to use the `Sovrin identity network` to enable its members to get transparency about who has fulfilled the criteria to be a member. But now the AOF does not issue Kilt VCs anymore.

And while the first 3 banks were willing to use the same identity system, the newest partner bank has already implemented a DID based system and is reluctant to switch.

##### Help is on its way

What is missing is a system which is DID method agnostic and allows to encode the rules in a machine readable, immutable and trustworthy manner. That is what the Trust Protocol provides.

The trust protocol enables the creation of complex compliance rules based on VCs from any DID method. The rules are stored in a blockchain and constitute a `policy graph` against which every Verifiable Presentation can be checked.

![Policy Graphs](https://res.cloudinary.com/mhrsntrk/image/upload/v1646837908/veri5/4_sp3nds.png)

The `policy graph` is versioned and contains full historiographic documentation. It is therefore always possible to answer the question: was this VC valid at the time of issuance?

> In the near future, the winners will be the organisations which are able to collaborate most efficiently. Creating publicly verifiable policy graphs is the most efficient way to build the trust relationships which are required for effective collaboration.
> 

With DIDs, users can authenticate without the need for an identity server but the authorisations are still stored in silos within the applications the users connect to. This leads to needless repeated registration and verification, adds friction to commercial processes and reduces security as one organisation can not learn from the revocations at their peers.

The verification process with the Policy Graph looks just slightly different:

![Verification w/Policy Graph](https://res.cloudinary.com/mhrsntrk/image/upload/v1646837908/veri5/5_vngje6.png)

#### Conclusion

In any software solution that requires users to authenticate, Identity and Access Management is a mandatory feature.

The identity system of the decentralised world will be self sovereign and the solutions for this have been implemented by many. But this is only the first half of the equation, the `I`

In order to create a truly decentralised ecosystem, we also need to provide a self sovereign Access Management solution; the `A`. This is what the Trust Protocol provides:

- Identity method agnostic
- Complex policy description
- Completely decentralised with no central database
- No ACL or other user membership list
- Cryptographically secure
- Usable on-chain, off-chain and cross-chain

### Project Details (Work all together)

// Waiting for Pablo & Micha for architecture diagram.

We expect the teams to already have a solid idea about your project's expected final state. Therefore, we ask the teams to submit (where relevant):

- Mockups/designs of any UI components
- Data models / API specifications of the core functionality
- An overview of the technology stack to be used
- Documentation of core components, protocols, architecture, etc. to be deployed
- PoC/MVP or other relevant prior work or research on the topic
- What your project is _not_ or will _not_ provide or implement
  - This is a place for you to manage expectations and to clarify any limitations that might not be obvious

### Ecosystem Fit

// To-do

Help us locate your project in the Polkadot/Substrate/Kusama landscape and what problems it tries to solve by answering each of these questions:

- Where and how does your project fit into the ecosystem?
- Who is your target audience (parachain/dapp/wallet/UI developers, designers, your own user base, some dapp's userbase, yourself)?
- What need(s) does your project meet?
- Are there any other projects similar to yours in the Substrate / Polkadot / Kusama ecosystem?
  - If so, how is your project different?
  - If not, are there similar projects in related ecosystems?

## Team :busts_in_silhouette:
### Team members

- Micha Roon (Research Lead)
- Pablo Buitrago (Team Lead)
- Mahir Şentürk (Product Owner) 
- Ezequiel Aranda (Quality Assurance Engineer)
### Contact

- **Contact Name:** Micha Roon
- **Contact Email:** micha.roon@verifive.io
- **Website:** https://verifive.io
### Legal Structure

- **Registered Address:** Avenue Warnery 8, CH-1007 Lausanne Switzerland
- **Registered Legal Entity:** managination LLC

### Team's experience

// To-do

Please describe the team's relevant experience. If your project involves development work, we would appreciate it if you singled out a few interesting projects or contributions made by team members in the past. For research-related grants, references to past publications and projects in a related domain are helpful.

If anyone on your team has applied for a grant at the Web3 Foundation previously, please list the name of the project and legal entity here.
### Team Code Repos

- https://github.com/veri5
- https://github.com/veri5/trust-protocol

GitHub accounts of all team members.

- https://github.com/drgorb
- https://github.com/changobuitrago
- https://github.com/mhrsntrk
- https://github.com/ezequielaranda

Substrate.stackexchange accounts of all team members.

- https://substrate.stackexchange.com/users/205/pablo-buitrago

### Team LinkedIn Profiles

- https://www.linkedin.com/in/micha/
- https://www.linkedin.com/in/changobuitrago/
- https://www.linkedin.com/in/mahirsenturk/
- https://www.linkedin.com/in/ezequielnaranda/
- https://www.linkedin.com/in/michalbacia/

## Development Status :open_book:

// We can add some information on why this is needed and nobody is working on it.

If you've already started implementing your project or it is part of a larger repository, please provide a link and a description of the code here. In any case, please provide some documentation on the research and other work you have conducted before applying. This could be:

- links to improvement proposals or [RFPs](https://github.com/w3f/Grants-Program/tree/master/rfp-proposal) (requests for proposal),
- academic publications relevant to the problem,
- links to your research diary, blog posts, articles, forum discussions or open GitHub issues,
- references to conversations you might have had related to this project with anyone from the Web3 Foundation,
- previous interface iterations, such as mock-ups and wireframes.

## Development Roadmap :nut_and_bolt:
### Overview

- **Total Estimated Duration:** 6 months
- **Full-Time Equivalent (FTE):** ~ 2 FTE
- **Total Costs:** 60,000 USD

### Milestone 1 — Policy Graph Demo 

- **Estimated duration:** 1 month
- **FTE:**  1
- **Costs:** 5,000 USD

| Number | Deliverable | Specification |
| -----: | ----------- | ------------- |
| 0a. | License | Apache 2.0 / GPLv3 / MIT / Unlicense |
| 0b. | Documentation | We will provide both **inline documentation** of the code and a basic **tutorial** that explains how a user can use BDD scenarios written in Gherkin to publish a `Policy Graph` and run queries. |
| 0c. | Testing Guide | Core functions will be fully covered by unit tests to ensure functionality and robustness. In the guide, we will describe how to run these tests. |
| 0d. | Docker | We will provide a Dockerfile(s) that can be used to test all the functionality delivered with this milestone. |
| 0e. | Article | We will publish an **article** that explains why Self-Sovereign Identity ecosystem needs `Policy Graphs` to be used as a trust/governance framework.
| 1. | Gherkin Interface | We will create example scenarios written in Gherkin to use it as an interface|
| 2. | neo4j | We will create a neo4j instance to store Policy Graphs it will allow us to publish/edit Policy Graphs |
| 3. | Graph Queries | We will create number of queries works on neo4j instance |


### Milestone 2 — Implement Policy Graphs Into Substrate

- **Estimated Duration:** 3 months
- **FTE:**  2
- **Costs:** 30,000 USD

| Number | Deliverable | Specification |
| -----: | ----------- | ------------- |
| 0a. | License | Apache 2.0 / GPLv3 / MIT / Unlicense |
| 0b. | Documentation | We will provide both **inline documentation** of the code and a basic **tutorial** that explains how a user can use BDD scenarios written in Gherkin to publish a `Policy Graph` to Substrate storage and edit it if necessary. |
| 0c. | Testing Guide | Core functions will be fully covered by unit tests to ensure functionality and robustness. In the guide, we will describe how to run these tests. |
| 0d. | Docker | We will provide a Dockerfile(s) that can be used to test all the functionality delivered with this milestone. |
| 0e. | Article | We will publish an **article** that explains how we use Substrate to store and interact with `Policy Graphs`.
| 1. | Substrate module: X |  |  
| 2. | Substrate module: Y |  |  
| 3. | Substrate module: Z |  |  
| 4. | Substrate chain |  |  

### Milestone 3 — Interface

- **Estimated Duration:** 2 months
- **FTE:**  2,5
- **Costs:** 25,000 USD

| Number | Deliverable | Specification |
| -----: | ----------- | ------------- |
| 0a. | License | Apache 2.0 / GPLv3 / MIT / Unlicense |
| 0b. | Documentation | We will provide both **inline documentation** of the code and a basic **tutorial** that explains how a user can interact with `Policy Graphs` using the custom markdown and the dApp. |
| 0c. | Testing Guide | Core functions will be fully covered by unit tests to ensure functionality and robustness. In the guide, we will describe how to run these tests. |
| 0d. | Docker | We will provide a Dockerfile(s) that can be used to test all the functionality delivered with this milestone. |
| 0e. | Article | We will publish an **article** that explains how to apply real-world scenarios into `Policy Graphs`.
| 1. | UI/UX Design & Wireframes| We would like to simplify user interaction on the UI level by researching on UX topics |
| 2. | | |
| 3. | | |
| 4. | | |

## Future Plans

#### Short Term Objectives
-
-

#### Long Term Objectives
-
-


## Additional Information :heavy_plus_sign:

**How did you hear about the Grants Program?:** Web3 Foundation Website

At the same time, we are applying to [Substrate Builder's Program](https://substrate.io/ecosystem/substrate-builders-program/) to get technical support grant on `Chains Track` from the Substrate team. 
