# **FunFair by Zini n’ Friends**

**Team:** Gwee Zi Ni, Michelle Ho Chia Xin, Tay Xin Ying&nbsp;

**Problem Statement:** Travel Planner

**Video Presentation:** \[[https://youtu.be/kBjFbEip0bo](https://youtu.be/kBjFbEip0bo)\]

**Presentation Slides (For animation purposes only — see video for full content):**&nbsp;

\[[https://drive.google.com/drive/folders/1lLnOI565IFmXs38RmcxVbwfttv6qlaJF?usp=sharing](https://drive.google.com/drive/folders/1lLnOI565IFmXs38RmcxVbwfttv6qlaJF?usp=sharing)\]

&nbsp;

## **1\. Project Overview**

# **The Problem**

Group travel is not simply an itinerary-generation problem. It is a **decision-making problem**.

When people travel together, each traveller brings different interests, budgets, personal constraints, and ideas of what makes a trip worthwhile. These differences don't always coexist peacefully — they can collide and compete for the one resource a trip can never create more of: **time**.

And when they collide, the outcome is rarely fair. Often, the same people keep giving in, while their needs are quietly and repeatedly overlooked — not because anyone decided that on purpose, but because nothing in the process ever surfaces it.

The question we kept returning to was:

> **What should happen when a group cannot fit everyone's priorities into the same schedule?**

## **Stakeholders**

* **Travellers** — want their priorities and personal constraints to be genuinely respected, not quietly traded away.  
* **The travel group** — needs to reach a decision without the disagreement souring the friendship or the trip.  
* **The platform (AI mediator)** — needs to balance individual preference against fixed commitments such as travel dates, bookings, and departure times.

## **Where Existing Tools Fall Short**

Existing travel planning tools already do a great deal well:

| Tool | What it does well |
| ----- | ----- |
| **Wanderlog** | Builds detailed, map-based itineraries and lets a group co-edit them in real time |
| **TripIt** | Excellent at organising bookings a traveller has already made |
| **Troupe** | Lets a group run a quick poll on which city or destination to pick |
| **Roamly** | Collects each traveller's preferences privately before generating a group itinerary |

None of these products offer a solution for the moment a real conflict happens within the group — when two people's genuine priorities overlap and someone has to lose something.

Collaborating on a shared document, or running a group poll, is not a structured way to reach a fair decision. A poll can still overlook minority needs, since it only measures which option gets the most votes, not how much any one person is giving up. And even preference-collection tools like Roamly stop at generating a plan — they don't handle what happens when that plan reveals a genuine clash. Quieter or more accommodating travellers can end up compromising over and over, trip after trip, without anyone — including themselves — ever noticing the pattern.

## **Our Focus**

Our project deliberately does not try to out-build existing tools at itinerary generation, booking aggregation, or expense-splitting — problems that are already reasonably well solved. We focus on the narrower, harder gap underneath all of them:

> **How can we help groups resolve travel preference conflicts fairly — without forcing anyone to compromise blindly, and without letting the majority automatically override an individual's high-priority preference?**

&nbsp;

## **Our Solution**

FunFair is a group travel planning platform built around preference conflict resolution. Travellers privately share their interests and identify up to two Golden Tickets — activities they would genuinely regret missing. FunFair first tries to fit everyone's protected preferences into a shared itinerary, only triggering negotiation when a genuine conflict occurs. It then proposes and ranks possible resolutions, with explicit consent required before any protected preference is sacrificed.

### **Feature Set**

&nbsp;

| Feature | Purpose |
| ----- | ----- |
| **Private Preferences** | Travellers independently mark each activity as **Want, Flexible, or Prefer Not**, before other people's opinions can influence their choices. |
| **Golden Tickets** | Each traveller identifies up to two **high-priority protected activities** that they would genuinely regret missing. |
| **AI Working Draft** | Builds an initial multi-day itinerary by attempting to fit travellers' Golden Tickets, preferences, and shared trip constraints into the available schedule. |
| **Conflict Detection** | Identifies a **genuine scheduling conflict** when protected choices cannot coexist within the same time window or itinerary constraints. For example, two protected activities may compete for the same afternoon window, making it impossible to include both before a fixed group commitment.&nbsp; |
| **Trade-off Options** | Generates several structurally different ways to resolve a conflict instead of forcing a single answer. Example options include:  **Third Way** — Replace both conflicting activities with a nearby shared alternative that partially satisfies both interests. **Compromise** — Visit both activities for shorter periods so neither preference is completely dropped. **Keep Your Pick** — Keep one traveller's protected activity while requiring the other traveller's consent to give up theirs. **Split & Reunite** — Let affected travellers pursue different activities temporarily, then reunite at a fixed group commitment. |
| **Private Ranking** | Affected travellers rank the proposed resolutions independently, reducing social pressure and allowing the system to capture their individual priorities. |
| **Fairness History** | Keeps track of previous compromises so the same traveller is not repeatedly expected to give up their protected preferences. This history is considered when FunFair recommends future conflict resolutions. |
| **Fairness-Aware Recommendation** | Evaluates possible resolutions based on travellers' private rankings, feasibility, and fairness history, helping the group reach a practical solution without repeatedly asking the same person to compromise. |
| **Consent Gate** | A protected preference cannot be sacrificed automatically. When a proposed resolution would remove someone's Golden Ticket, the affected traveller must explicitly consent before it can be applied. |
| **Itinerary Rebalancing** | Rebuilds the affected part of the itinerary after a decision is accepted, so travellers do not have to manually reconstruct their schedule. |
| **Mystery Box** | Recommends a surprise, theme-based destination that fits an open slot when travellers are unsure what to do next, adding spontaneity without breaking the itinerary. |
| **AI Re-plan** | Adapts the itinerary when circumstances change, such as weather, tiredness, budget constraints, or a new user request, without requiring the entire trip to be rebuilt. |
| **Travel Handbook Export** | Converts the final itinerary into a printable travel handbook containing cultural notes, food recommendations, and fun facts for selected stops. |

&nbsp;

&nbsp;

## 

## **2\. Ideation & Process**

### **2.1 Ideas We Considered**

Table of every distinct idea generated, with why each was kept or dropped, order it so that chosen ideas are listed first

## **A. Core Framing**

| Idea | Status | Reason |
| ----- | ----- | ----- |
| Tinder-style voting destination (swipe yes/no, majority wins) | ❌ Dropped | There is no preference-strength signal. Some enthusiastic travellers might vote yes to most destinations, which could bias the itinerary and cause minority preferences to be overlooked. |
| Honest Itinerary Engine — constraint-satisfaction model (identify must-haves / nice-to-haves / deal-breakers \+ budget, solved as one optimization) | ✅ Kept | Solves for group-optimal fit instead of just tallying votes. This became the project's foundational philosophy. |

## **B. Preference-Strength Capture**

| Idea | Status | Reason |
| ----- | ----- | ----- |
| Heart-betting economy (❤️ \+ 🛡️, limited resource, secretly allocated to activity) | ❌ Dropped | Conflated enthusiasm with actual priority — extroverts may overstate their preferences, while people-pleasers may understate theirs. |
| Different destinations have different costs. Users are given a limited number of “backpacks” and allocate them to destinations with different backpack costs.&nbsp; | ❌ Dropped | System-assigned costs introduced a feasibility bias into what should be a pure preference signal based on the user's own judgement. |
| Heart Allocation (spend 1–5 hearts per Want item, using a limited heart budget) | ❌ Dropped | The mentor flagged it as too complex, and the team later found that it did not justify its complexity once Clash Cards were redesigned to trigger only on genuine conflicts rather than similar heart scores. |
| Super-Like merged into Swipe (cap of 2, replacing a separate Golden Ticket step) | ❌ Dropped | Created a secretary / optimal-stopping problem — users would have to decide whether to “spend” a Super-Like before seeing all available options. |
| Swipe (Want / Flexible / Prefer Not) \+ separate Golden Ticket step (max 2, chosen *after* swiping finishes) | ✅ Kept | Captures general preferences first, then allows users to identify their true priorities after seeing all available options. |

## **C. Conflict Detection Logic**

| Idea | Status | Reason |
| ----- | ----- | ----- |
| Trigger a forced choice when two of a person's own heart scores are similar | ❌ Dropped | Logically unsound — liking two activities equally does not mean they are actually in conflict. |
| Trigger a conflict only when there is a genuine scheduling or feasibility collision between two Golden Tickets | ✅ Kept | Matches what “conflict” actually means and became one of the most important corrections to the negotiation engine. |

## **D. Conflict Resolution Options**

| Idea | Status | Reason |
| ----- | ----- | ----- |
| Pay or compensate the person who sacrifices their preference | ❌ Dropped | Felt too transactional and could turn goodwill between friends or family into a market-like exchange. |
| Third Way (a different activity satisfying the underlying need behind both original choices) | ✅ Kept | Can provide common ground without fully favouring either side, partially satisfying both affected travellers. |
| Split & Reunite (the group temporarily splits for that time slot and reunites later)&nbsp; | ✅ Kept | Preserves both protected preferences without requiring either traveller to sacrifice their choice.&nbsp; |
| Compromise (sacrifice your own choice to preserve another person's)&nbsp; | ✅ Kept | Allows a traveller to voluntarily give up their own protected choice so another traveller can keep theirs. The sacrifice is recorded as a Compromise Coin and considered in future conflicts.&nbsp; |
| Keep Your Pick (the group stays together at one person's choice) | ✅ Kept | Only allowed behind the Consent Gate — it is never applied automatically. |

## **E. Fairness Memory**

| Idea | Status | Reason |
| ----- | ----- | ----- |
| Single Compromise Coin / fairness-history ledger | ✅ Kept | One source of truth, feeds directly into the trade-off scoring formula's fairness weight. |
| Compromise Coin shown on its own dedicated Ledger screen | ❌ Dropped | Based on mentor feedback, it was simplified and integrated into the flow as an inline message instead of requiring a dedicated screen. |

## **F. Governance — Who Decides?**

| Idea | Status | Reason |
| ----- | ----- | ----- |
| Trip creator decides conflicts unilaterally | ❌ Dropped (considered, never built) | Recreates the "loudest voice wins" problem at the group level — exactly what the project aims to avoid |
| Private ranking, limited to only the affected members, followed by a suggested solution generated using trade-off scoring formula | ✅ Kept | Avoids both majority override and single-person decision-making while giving affected travellers greater control over the outcome. |
| Consent Gate — a protected preference can never be sacrificed automatically | ✅ Kept | Directly protects the "genuinely respected" promise; declining falls back to Split & Reunite instead of forcing the sacrifice through. |

## **G. Flow Structure & Gamification**

| Idea | Status | Reason |
| ----- | ----- | ----- |
| Secret Mission (each traveller secretly names "one thing that would make this trip worth it," revealed at the end) | ❌ Dropped to stretch goal | The core loop is already self-contained without it; not worth the added complexity for the MVP. |
| A fixed flow that every trip must complete in full, including heart allocation and a 2-choose-1 decision when heart scores are similar, regardless of whether a real disagreement exists | ❌ Dropped | Too heavy for a low-conflict, casual trip and forces unnecessary negotiation. . |
| Progressive disclosure — full negotiation machinery (Clash Cards, Trade-off Board) only activates when the AI detects a genuine disagreement | ✅ Kept | Complexity appears only when a real conflict occurs, rather than being imposed on every user. |
| One-time "blind-box" reveal animation explaining why each stop made the cut | ❌ Dropped | The explanation disappeared after the animation, making it less useful once travellers were actually using the itinerary. |
| Tap-to-expand reasoning built directly into the itinerary, available any time | ✅ Kept | Keeps AI reasoning accessible while allowing the interface to remain clean when the explanation is collapsed. |

## **H. Post-Mentor Additions**

| Idea | Status | Reason |
| ----- | ----- | ----- |
| Trip Home screen (today's snapshot \+ entry points, separate from the full itinerary) | ✅ Kept | Added directly from mentor feedback ("show the ongoing itinerary on a homepage"). |
| AI Re-plan (weather / tired / budget / custom triggers, re-runs the same negotiation engine on a new constraint) | ✅ Kept | Added from mentor feedback and deliberately reuses the existing planning engine instead of requiring users to rebuild the itinerary manually. |
| Mystery Box (roll a themed, surprise-but-feasible activity into any open slot) | ✅ Kept | Gives travellers a lightweight way to fill gaps or handle moments when the group is unsure what to do next. |
| Export as Travel Handbook (real client-side PDF booklet, photos \+ culture/history/food notes, ordered by the finalized itinerary) | ✅ Kept | Makes the trip more immersive and turns the itinerary into a more engaging travel companion. |
| Change the metrics from numerical scores to categories | Kept | Makes the results easier for users to understand and avoids giving prototype metrics a false sense of precision.&nbsp; |

## 

### **2.2 Ideation Boards**

![Problem Tree](https://github.com/gweezini/CodeNection_FunFair-Travel-Planner/blob/main/ProblemTree.jpg)  

This board shows our core problem: travellers have different priorities that cannot fit into just one schedule. It explains how limited time and different budgets lead to silent unhappiness and damage friendships during the trip.

![Scamper](https://github.com/gweezini/CodeNection_FunFair-Travel-Planner/blob/main/Scamper.jpg)  

We ran a SCAMPER session to explore different ways to solve schedule clashes. It shows our team's creative process, including bad ideas we dropped (like total AI control) and good ones we kept (like the Consent Gate).  

&nbsp;

### **2.3 Mentor Consultation**

| Date | Mentor | Feedback Received | What Was Changed |
| :---- | :---- | :---- | :---- |
| 9/9/2026 | Zach Khong | The Heart Allocation step before Golden Tickets often gave very similar heart values across different activities. When the itinerary could not fit everything, the app still forced travellers to choose between activities that had almost the same priority. Since Golden Tickets were already the activities that travellers considered as “must-go”, this made travellers choose again between activities they had already shown as their top priorities.  The trade-off screen required travellers to read a separate explanation for each option, such as Third Way and Split & Reunite, on a different page before they could vote. This added an unnecessary step before making the actual decision.  The satisfaction score was shown as a raw fraction, such as “4/4”. Testers felt that the number alone did not clearly explain what the group had achieved and could seem like an arbitrary number.  The Compromise Coin did not need its own dedicated screen to show both travellers’ coin changes, such as “me \+0, Alice \+1”. This information could be handled in the background instead.  When a trip is already ongoing, the homepage should show the current itinerary directly instead of requiring travellers to navigate to it manually.  Weather was not included in the itinerary, which missed an opportunity to demonstrate the AI Re-plan feature.&nbsp; | The Heart Allocation step was removed completely. Travellers now go directly from swiping to naming their Golden Tickets. This removes the extra and unnecessary step of prioritising the activities again.  The explanation and voting were combined into one screen. The main option, such as “Keep your pick”, is shown first, while the alternative options are shown in smaller text underneath. Travellers can tap the alternative options to vote immediately without going through a separate explanation and voting process.  The raw score was replaced with category labels, such as “Compatible”. This allows the result to show the type of outcome the group achieved instead of only showing a number.  The separate Compromise Coin screen was removed. Only the affected traveller’s coin change is shown through a small popup. The current user’s own point-of-view change is tracked silently by the backend without showing a separate screen.  The system now calculates the current trip day based on the traveller’s arrival and return flight dates, such as Day 2\. When travellers open the itinerary, it will directly show the schedule for the current day.  A mocked weather forecast was added for each day in the itinerary. The weather information is now used to briefly demonstrate the AI Re-plan flow. For example, a bad weather forecast can trigger the rescheduling mechanism, which is shown lightly in this version.&nbsp; |
| 11/9/2026 | Zach Khong |  |  |

Even if you disagreed with a piece of feedback, you can say so and explain why. You will not be penalised for doing something against a mentor’s advice, it will still count as engaging with it.

## **3\. Design & Prototype**

**UI Prototype:**[https://funfairplanner.netlify.app/](https://funfairplanner.netlify.app/)&nbsp;

| Group Constraints  ![Constraints](https://github.com/gweezini/CodeNection_FunFair-Travel-Planner/blob/main/Constraint.png)| Before any personal preference is collected, the group locks shared, non-negotiable constraints — trip dates, a hard airport deadline, and a fixed Day 2 dinner. Individual budgets are handled privately in the next step.&nbsp; |
| ----- | :---- |
| **Preference Swipe** ![][image4] | Each traveller privately swipes every activity into Prefer Not / Flexible / Want, one card at a time, before seeing anyone else's choices.&nbsp; |
| **Golden Tickets** ![][image5] | From their own Wants, each traveller chooses up to 2 protected picks and can see what the rest of the group has already chosen, helping to identify possible clashes early.&nbsp; |
| **Schedule Conflict** ![][image6] | The AI's working draft flags the moment two protected Golden Tickets. For example, Yanaka Cultural Walk and Harajuku Shopping — compete for the same window ahead of a fixed dinner.&nbsp; |
| **Trade-off & Private Ranking** ![][image7] | Four structurally different resolutions are shown together with brief trade-offs, and each traveller ranks them privately on the same screen. There is no need for a separate explain-then-vote flow.&nbsp; |
| **Best Shared Fit** ![][image8] | The result is expressed as categorised labels (Group fit, Priorities, Balance, Practicality) instead of a raw score, so the outcome reads as meaning, not an arbitrary number.&nbsp; |
| **Compromise Logged** ![][image9] | When a protected slot is yielded, the trade is confirmed and a Compromise Coin is credited to that traveller's balance. Coins carry forward: a traveller who has already sacrificed more accumulates priority, making them more likely to win the next genuine trade-off — this is what turns "fairness" into something mechanical rather than just a feeling.&nbsp; |
| **Finalized Itinerary \+ Weather** ![][image10] | The settled itinerary shows live per-day weather alongside Add Stop and Re-plan controls, so a forecast change can trigger an AI Re-plan directly from here.&nbsp; |
| **Mystery Box Destination** ![][image11] | Tapping Add Stop on any open slot offers a Mystery Box: travellers pick a theme and choose whether to roll a Group surprise (everyone shares the reveal) or a Personal one, then roll a random destination straight into the gap instead of leaving it blank.&nbsp; |
| **Trip Summary and Travel HandBook**![][image12] | The finalised trip may be turned into a keepsake PDF, including a cover page, a one-page itinerary index, and a dedicated page for each stop. Each page includes information about the local culture and history, a “while you’re there” tip, a local food recommendation, and a fun fact.&nbsp; |

&nbsp;

## **4\. What Makes It Different**

Most AI travel planners focus on generating and organising itineraries. FunFair focuses on resolving preference conflicts when important group priorities cannot all fit into the same schedule.

&nbsp;

Core Innovations:

| Feature | What Makes It Different |
| ----- | ----- |
| **Golden Tickets** | Instead of treating every preference equally, each traveller can protect up to two activities they would genuinely regret missing. This creates a clear distinction between ordinary interests and high-priority preferences. |
| **Genuine Conflict Detection** | FunFair does not trigger negotiation simply because travellers want different things. A conflict is raised only when protected choices cannot realistically coexist within the same schedule or trip constraints. |
| **Multiple Resolution Strategies** | Rather than generating one “best” answer, FunFair explores structurally different resolutions such as **Third Way**, **Compromise**, **Split & Reunite**, and **Keep Your Pick**. |
| **Private Ranking** | Affected travellers rank possible resolutions independently, reducing social pressure and preventing more outspoken members from dominating the decision. |
| **Fairness-Aware Recommendation** | Feasible resolutions are evaluated using **private rankings, group-level preference preservation (how many other golden tickets can be protected), feasibility, and fairness history**, instead of relying only on majority preference. |
| **Fairness History** | Previous sacrifices are remembered and considered in later decisions, reducing the chance that the same traveller repeatedly has to give up what matters to them. |
| **Consent Gate** | AI can recommend a resolution, but it cannot automatically sacrifice someone's Golden Ticket. If a protected preference would be lost, the affected traveller must explicitly consent first. |
| **Conflict-to-Rebalance Loop** | Once a decision is accepted, FunFair updates the affected itinerary around that outcome instead of leaving the group to manually rebuild the schedule. |

&nbsp;

> **The key difference is not preference collection, but preference conflict resolution.**

&nbsp;

&nbsp;

Comparison:

&nbsp;

&nbsp;

| Capability | Wanderlog | TripIt | Roamly | FunFair |
| ----- | ----- | ----- | ----- | ----- |
| Itinerary planning | ✓ | ✓ | ✓ | ✓ |
| AI-assisted planning | ✓ | Limited | ✓ | ✓ |
| Group collaboration | ✓ | ✓ | ✓ | ✓ |
| Private preference collection | — | — | ✓ | ✓ |
| Protected priorities | — | — | — | **✓** |
| Conflict-resolution strategies | — | — | Not primary focus | **✓** |
| Private ranking | — | — | — | **✓** |
| Fairness history | — | — | — | **✓** |
| Consent before sacrifice | — | — | — | **✓** |
| Rebalancing after conflict | Some replanning | — | AI editing | **✓** |

&nbsp;

*Roamly also uses traveller preferences to support group itinerary generation, while FunFair focuses on **what happens when those preferences still cannot be reconciled**.*&nbsp;

### **Our Key Twist**

FunFair shifts AI from being the **decision-maker** to being the **facilitator**.

Instead of:

**Preferences → AI generates itinerary**

FunFair follows:

**Private Preferences → Golden Tickets → Shared Draft → Genuine Conflict → Resolution Options → Private Ranking → Fairness-Aware Recommendation → Consent → Rebalanced Itinerary**

AI recommends; humans consent.&nbsp;

### **Supporting Features**

* **Mystery Box** — suggests a surprise but feasible activity for open slots.  
* **AI Re-plan** — adapts the itinerary when circumstances change.  
* **Travel Handbook Export** — turns the itinerary into a travel booklet with cultural and food information.

&nbsp;

## **5\. Technical Architecture & Feasibility**

**Tech stack**

&nbsp;

| Layer | Technology | Why we chose it | Constraints to expect |
| :---- | :---- | :---- | :---- |
| Frontend | [Next.js](http://Next.js/) \+ React \+ TypeScript | Component-based development suits FunFair's multi-step flow, including preferences, conflict resolution, consent, and itinerary editing. TypeScript also helps keep trip and preference data structured and consistent. | The current prototype is built with HTML/CSS/JavaScript, so the MVP will migrate the core flow incrementally rather than rebuilding every feature at once.&nbsp; |
| UI / Styling | CSS \+ Tailwind CSS | Allows rapid development of responsive mobile-first interfaces while maintaining consistent styling across the application. | Custom interactions such as drag-and-drop ranking and animated Mystery Box elements may still require additional CSS/JavaScript. |
| Backend | Next.js API Routes / Server Actions | Keeps the frontend and backend in one project and provides a secure layer for database and external API requests. | API keys must remain server-side, and serverless execution limits may affect long-running AI operations. |
| Database & Authentication | Supabase (PostgreSQL \+ Supabase Auth) | Stores users, trips, preferences, Golden Tickets, private rankings, decisions, and fairness history while supporting user authentication. | Free-tier limits may apply, and database access rules must be configured correctly to prevent travellers from viewing private rankings or preferences. |
| Conflict & Fairness Engine | Server-side TypeScript rules and scoring logic | Handles hard constraints, genuine conflict detection, feasibility filtering, preference preservation, fairness history, and consent deterministically instead of relying entirely on AI. | The MVP will use a limited and explainable scoring model rather than a complex optimisation system. |
| AI Assistance | Gemini API | Assists with itinerary suggestions, trade-off alternatives, explanations, and AI Re-plan. | AI outputs may be inconsistent, so hard constraints and consent rules should be enforced by application logic rather than trusted entirely to the model. |
| Map & Destination Display&nbsp; | MapLibre GL JS \+ OpenStreetMap data&nbsp; | Provides an interactive map for displaying destinations and itinerary stops without depending on a proprietary mapping platform. MapLibre supports markers, layers, and route visualisation, while OpenStreetMap provides geographic map data. | MapLibre handles map rendering rather than routing or place discovery. The MVP will use a curated Tokyo destination dataset, while additional services can be added later for dynamic search. |
| Travel-Time feasibility | openrouteservice API | Provides route distance and estimated travel time between activities, helping FunFair determine whether two Golden Tickets can realistically coexist within the same schedule. | API request limits may apply. If unavailable, the prototype can fall back to predefined travel-time estimates for selected Tokyo destinations. |
| Weather | Open-Meteo Forecast API | Provides forecast data for weather-triggered itinerary re-planning and is simple to integrate for a prototype. | Forecasts may be inaccurate or unavailable, so weather is treated as a replanning signal rather than a guaranteed condition. |
| Travel Handbook Export | jsPDF | Generates the Travel Handbook directly in the browser without requiring a separate PDF-generation service. | Emoji and unsupported fonts require special handling, while remote images may face CORS restrictions. |
| Hosting | Vercel | Integrates naturally with Next.js and provides simple deployment for the hackathon MVP. | Free-tier serverless and bandwidth limits should be considered if usage grows. |

&nbsp;

### **Core Decision Logic**

FunFair does not rely entirely on generative AI to decide what the group should do.

Hard constraints are checked first and infeasible resolutions are removed before recommendation. The remaining options are evaluated using a prototype scoring model based on:

**Private Ranking \+ Group Level Preference Preservation \+ Fairness History \+ Feasibility**

The prototype currently uses these factors to recommend the strongest shared fit, while **explicit consent remains mandatory if the chosen resolution sacrifices a protected Golden Ticket**.

This separation allows AI to assist with recommendations while deterministic application rules continue to enforce important constraints.

&nbsp;

&nbsp;

**System architecture diagram** (Optional, if you feel it would help the reviewers understand your architecture better)

![][image13]

### 

### 

### **System Architecture Explanation**

This diagram shows how information moves through FunFair, from collecting individual traveller inputs to producing a shared itinerary.

Travellers first submit their private preferences, Golden Tickets, and personal constraints through the FunFair frontend. The information is stored in Supabase and processed together with supporting data from the Maps and Places API, Weather API, and LLM API.

The Planning and Conflict Engine uses these inputs to build a feasible group itinerary. If all protected preferences can coexist, the itinerary is generated directly. If a conflict is detected, the affected travellers proceed to the trade-off process.

Private rankings and fairness history are then used to generate a fairness-aware recommendation. If the recommended option would sacrifice a Golden Ticket, it must pass through the Consent Gate before the itinerary can be updated.

Once a resolution is accepted, the affected schedule is rebalanced and added to the shared itinerary. Travellers can then access AI Re-plan, Mystery Box, and Travel Handbook Export.

### **Current Prototype and Future Implementation**

The current prototype is developed using HTML, CSS, JavaScript, and jsPDF. It uses predefined traveller profiles, destination data, weather scenarios, and conflict examples to demonstrate the complete user flow.

During the building phase, we plan to migrate the application to Next.js and connect it to Supabase for data storage and authentication. Maps, Weather, and LLM APIs may also be integrated to provide destination information, weather updates, itinerary suggestions, and trade-off explanations.

## **Build Plan & Scope**

During the building phase, we will develop FunFair as a functional mobile-first web application that demonstrates the complete preference-conflict resolution loop. Our priority is to build the core mechanism reliably rather than attempting to create a full commercial travel platform within the hackathon period.

### **Core MVP Scope**

The MVP will support one shared trip involving multiple travellers. Each traveller will be able to:

* Join or create a trip.  
* Enter personal constraints and an individual budget.  
* Privately classify destinations as Want, Flexible, or Prefer Not.  
* Select up to two Golden Tickets from their Want list.  
* View an AI-generated group itinerary based on the group's preferences and fixed constraints.  
* Receive a conflict alert when two protected activities cannot fit within the same schedule.  
* Privately rank feasible resolution options.  
* Review a fairness-aware recommendation.  
* Give or decline consent when a proposed outcome would remove their Golden Ticket.  
* View the rebalanced itinerary after an outcome is accepted.  
* The Mystery Box was added in response to the current popularity of blind-box and surprise-discovery experiences. It introduces spontaneity into the planning process by recommending a surprise destination based on the traveller's selected theme. Unlike a completely random suggestion, the destination must still fit the available itinerary slot and existing trip constraints.

The system will also store each traveller's previous voluntary sacrifices as fairness history. This allows later conflict recommendations to consider whether the same person has already compromised before.

### **Conflict-Resolution Engine**

The core engine will follow a rule-based process:

1. Treat fixed bookings, travel dates, budgets, accessibility needs, and departure deadlines as hard constraints.  
2. Attempt to place all Golden Tickets into feasible time windows.  
3. Trigger negotiation only when protected preferences genuinely cannot coexist.  
4. Remove options that violate hard constraints before ranking begins.  
5. Evaluate the remaining options using:  
   * Private ranking: 40%  
   * Group Level Preference Preservation: 30%  
   * Fairness history: 20%  
   * Practical feasibility: 10%  
6. Require explicit consent before removing an affected traveller's Golden Ticket.  
7. Update the affected itinerary and fairness history only after the decision is accepted.

The LLM may assist with explanations, alternative activities, and itinerary suggestions. However, hard constraints, consent requirements, and fairness-history updates will be enforced by the application's own logic instead of relying entirely on AI-generated output.

### **Scope Limits**

To keep the project realistic within the hackathon period, the MVP will not attempt to provide:

* Flight, hotel, attraction, or restaurant booking.  
* Payment processing or expense splitting.  
* Real-time ticket availability or price comparison.  
* Complete worldwide destination coverage.  
* Production-level route optimisation for every possible location.  
* Fully autonomous AI decision-making.  
* A native iOS or Android application.

The MVP may use a curated Tokyo destination dataset and mocked or limited external data where necessary. This allows us to focus testing on FunFair's main innovation: fair preference-conflict resolution.

### **Development Timeline**

&nbsp;

| Timeline | Focus | Planned Work | Expected Output |
| ----- | ----- | ----- | ----- |
| **21–27 Sep** | **Foundation & Core Flow** | Migrate the existing prototype into **Next.js \+ TypeScript** components. Set up **Supabase** for users, trips, preferences, Golden Tickets, rankings, and fairness history. Implement the core **preference → Golden Ticket → draft itinerary** flow. | Functional frontend structure, persistent trip data, and the first half of the core user journey. |
| **28 Sep–4 Oct** | **Conflict Resolution Engine** | Implement genuine conflict detection and feasibility filtering. Add private ranking, fairness-aware scoring, Consent Gate, and itinerary rebalancing. Integrate **openrouteservice** for travel-time feasibility. Integrate **Gemini API** for itinerary suggestions and trade-off explanations. | Complete end-to-end conflict-resolution loop with real decision logic. |
| **5–11 Oct** | **Supporting Features, Testing & Deployment** | Integrate **Open-Meteo** for a limited weather-based re-planning flow.  Add **MapLibre GL JS \+ OpenStreetMap** for itinerary visualisation. Retain **jsPDF** for Travel Handbook export. Refine Mystery Box and AI Re-plan if time permits. Conduct user-flow testing, fix edge cases, polish the mobile UI, and deploy on **Vercel**. | Stable, deployable MVP ready for final demonstration. |

&nbsp;


[image13]: FunFair_flow_colorful.gif
