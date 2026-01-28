# Behavioral Interviews

I’m a software developer with around 10 years of experience, mostly focusing on iOS development. Lately I’ve been exploring other areas of the tech stack, at my last company I started picking up backend tasks and driving some architecture decisions. Today I’m working as a full time backend .Net developer.

I’m exploring my options and looking for more customer centric front end roles. I find working towards a customer experience of an application way more rewarding than fiddling with the database, though I am glad to know how the backend works. 

# Experiences

---

## Airline Company

- **Offers External API Service**
    - Additions made for Self Service URL + Feeds API
- (ALL TASKS) **Adding loyalty account info as an offer evaluation criteria**
    - Start by reaching out to other teams to gather info about how the data looks from their end.
    - create a meeting if needed to go through technical requirements
        - can this be done through an api? Does it need a RMQ message
        - Can we subscribe to existing lists, can we handle the traffic / is it all relevant to us?
    - sync back up with manager to explain proposal, get sign off from him
    - work on Contract version so all teams can work in parallel

## Biiibo

- [Payments Refactor](Biiibo%20Accomplishments/Payments%20Refactor%20162a1339f88a809585e7c8bef399ce41.md)
    - Tech spec: Flow charts What does the code look like today
    - What is the desired outcome
    - Stage 1: Logical refactor to all use a single flow
    - Stage 2: rename / change the location of our payment object storage
    - Stage 3 Optional: Change our business workflow to match ERP’s expected flow as stated on their documentation.
- [Homepage Row vs Dynamic Row](Biiibo%20Accomplishments/HomepageRow%20vs%20DynamicRow%20162a1339f88a80109649c486bf63c183.md)
    - I recognized a new feature request as an extension of other features we have already done
    - dynamic content was headed towards each page having its own ‘type’ having to redo many features we had basically already done
    - I redirected us to writing reusable components instead, and then each generic page could be made up of a collection of components.
- [Lazy Loading Frappe Docs](Biiibo%20Accomplishments/Lazy%20Loading%20Frappe%20Documents%20175a1339f88a80fdbf6aff99842dd12d.md)
    - We were passing dictionaries from function to function, tightly coupling their usage and driving me nuts. I would constantly point out in PRs asking for the usage of objects
    - When using frappe’s ‘get list of’, would always return a dict instead of an object
- [Rolling back + Atomic Operations](Biiibo%20Accomplishments/Rolling%20back%20+%20Atomic%20Operations%20in%20ERP%20175a1339f88a80f791f7eb4b22fe8034.md)
    - We were rewriting the payment portion of the backend, needed multiple operations to be Atomic
    - Enforced consistent usage of Get and Post, and Throwing Errors.

## TribalScale

- **Enforcing Error propogation**
    - Convince the stakeholders that seeing more errors in an application is actually beneficial both to development and to its users
- **State Machine via GRPC**
    - Noticed an occasional inconsistency in vehicle state { locked, parked, waiting for request, pathfinding, picking up passenger, dropping off passenger, … }
    - States managed between a mix of sending API calls and recieving Grpc messages
    - **Initiated Tech Discussions: Brought to the team that we needed to keep track of our own internal state, we are recieving bad data sometimes.**
        - EX. We push ‘picked up passenger’ via API call, we would expect certain states and would have to throw away others
        

## WGames

## VitalHub

## **S – Situation**

“we were building a feature that let users save offline media”

## **T – Task**

“My role was to own implementation”

## **A – Action**

“I drafted a new API integration plan with the backend team, documented what could be reused, and highlighted what had to be rewritten.”

## **R – Result**

“We renegotiated deadlines and delivered a product with plans to replace existing logic in the future”

# Generic

## Conflicts

- Optional behavior in converters / adapters in backend role.
    - Sometimes upstream ended up passing unexpected nulls, and doing this defensively saved production issues.
    - consistency is important, but sometimes being pragmatic wins.

## Pivot?

- offers API

## **tradeoff between technical quality and delivery speed**

- Offers External API Service

## **challenging bug or production issue**

- Rolling back + Atomic Operations?
- Self Service URL missing
    - during initial deployment and QA testing there was an issue with URLs not showing up
    - mismatch on character case of RecordLocators.
    - inserted datadog logs to view the data we were getting from external services, as it must differ from what I mock locally

---