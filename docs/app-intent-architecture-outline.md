PantryPal

Initial Intent and Architecture Outline

1. Purpose

PantryPal is a household food planning assistant designed to make everyday meal planning, shopping and food tracking easier.

The idea is simple: most households are already managing food across several disconnected places. There is the weekly supermarket shop, the shared shopping list, food already sitting in the fridge or pantry, meal-kit services like My Food Bag, personal preferences, budget pressure, and sometimes individual food tracking.

PantryPal brings those pieces together in one practical place.

At this stage, this document is not a final architecture. It is an initial intent and outline document to help shape the product direction, clarify the important requirements, and provide a foundation for the application architecture that will follow.

⸻

2. Product intent

PantryPal should help a household answer four everyday questions:

1. What are we eating this week?
2. What do we already have?
3. What do we need to buy?
4. What did I actually eat, if I want to track it?

The product should feel useful before it feels clever.

The aim is not to build another recipe app or a strict calorie-tracking tool. The aim is to create a simple household assistant that supports real-life food decisions.

PantryPal should help people plan meals, use what they already have, shop around specials, account for My Food Bag meals, reduce waste, and make personal food tracking easier with less manual effort.

⸻

3. Working product statement

PantryPal is a shared household meal and shopping assistant that helps people plan meals around what they already have, what is arriving through services like My Food Bag, what is on special at local supermarkets, and what each person likes or wants to track.

A simple positioning line could be:

PantryPal — meals, lists and leftovers sorted.

Or:

Plan meals, shop smarter, and make the most of what you already have.

⸻

4. What problem are we solving?

Food planning is usually fragmented.

A household might have:

* a supermarket app
* a paper or Notes shopping list
* My Food Bag meals arriving during the week
* food already in the fridge
* pantry staples that may or may not be there
* one person tracking calories or meals
* another person doing the shopping
* changing weekly specials
* leftovers that either get used or forgotten

Each part makes sense on its own, but the overall experience is messy.

The result is familiar:

* duplicate items are bought
* food gets wasted
* people still ask “what’s for dinner?”
* shopping lists are incomplete
* specials are hard to use properly
* meal tracking takes extra effort
* My Food Bag meals are not always considered when planning the rest of the week

PantryPal should reduce that friction.

⸻

5. What PantryPal should do

At its simplest, PantryPal should support three connected spaces:

Meals

This is where the household plans what it is eating.

Meals may come from:

* home-cooked recipes
* My Food Bag
* leftovers
* ready-made meals
* takeaway
* eating out
* simple repeat favourites

List

This is the shared shopping list.

It should show what needs to be bought, who added it, what meal it relates to, whether it is on special, and whether the household may already have it.

Kitchen

This is a lightweight view of what is already in the fridge, pantry or freezer.

It should not behave like strict stock management. It should help the household make better decisions without creating more admin.

⸻

6. What makes PantryPal different

PantryPal should not start with recipes.

It should start with the household.

That means it should understand:

* what meals are already covered this week
* what food is likely already available
* what the household usually eats
* what people like and dislike
* what needs to be bought
* what is currently on special
* what each person may want to track privately

The difference is not that PantryPal can generate meals. Many tools can do that.

The difference is that PantryPal should generate useful meal and shopping decisions based on the real operating context of the household.

⸻

7. Intended users

PantryPal has a few different user types.

The same person may play more than one role.

Household organiser

The person who thinks ahead and wants the week to feel easier.

They need quick meal planning, a reliable shared list, and less duplicated effort.

Shopper

The person in the supermarket or ordering online.

They need a clear, up-to-date list that is easy to use on a phone.

Household contributor

The person who wants to add milk, snacks, toothpaste, or lunch items without dealing with the whole meal plan.

They need the app to be simple and fast.

Food tracker

The person who wants to track what they eat without manually typing every meal from scratch.

They need planned meals, portion options, personal estimates, and private logging.

Budget-conscious user

The person trying to make better use of specials and avoid waste.

They need practical suggestions, not generic advice.

⸻

8. Initial product principles

The following principles should guide early design and architecture decisions.

8.1 Household-first

PantryPal should solve shared household food planning first.

The shared list, meal plan, and kitchen view are the core household experience.

8.2 Personal-private

Personal food tracking should be private by default.

A household can share a meal plan without sharing each person’s calorie log, symptoms, weight goals or eating notes.

8.3 The shopping list is the action layer

The shopping list is where plans become practical.

Meal planning, pantry tracking, specials, and My Food Bag inputs should all improve the list.

If a feature does not make the list, the meal plan, or the tracking experience easier, it should be challenged.

8.4 AI should assist, not take over

AI can suggest meals, substitutions, list items and food log estimates.

But people should stay in control.

The app should explain why something was suggested and make it easy to accept, reject or correct.

8.5 Approximate is acceptable, but it must be transparent

The app will not always know exactly what is in the fridge, whether a special is still available, or how many calories were in a homemade meal.

That is okay, as long as the app is honest about uncertainty.

Estimated prices, likely pantry items and calorie approximations should be clearly labelled.

8.6 Useful without deep integrations

The app should still work even if there is no official supermarket API, no My Food Bag API, and no direct cart integration.

Manual entry, screenshot upload, receipt import and copy-paste flows should be treated as valid product experiences, not poor fallbacks.

8.7 Mobile-first

PantryPal needs to work in the kitchen and in the supermarket.

The shopping list must be fast, simple, and reliable on a phone.

8.8 Gentle, not judgmental

Food tracking should feel supportive, not punishing.

The app should avoid shame-based language, strict diet framing, or unnecessary warnings.

⸻

9. Initial functional requirements

The early requirements can be grouped into seven areas.

⸻

9.1 Household and sharing

PantryPal should allow users to create a shared household space.

The household space should support:

* creating a household
* inviting other people
* viewing shared meal plans
* viewing and updating shopping lists
* adding pantry or fridge items
* adding household preferences
* managing basic roles and access

The household experience should be easy enough that someone can join just to use the shopping list.

Not every household member should need to care about meal planning or food tracking.

⸻

9.2 Shared shopping list

The shopping list is a core feature.

It should support:

* adding items manually
* adding items from planned meals
* adding household items not linked to meals
* ticking items off
* editing quantities
* adding notes
* grouping by category
* showing who added an item
* linking an item to a meal
* sharing the list outside the app
* working reliably in the supermarket

The list should be able to include both food and non-food items.

For example:

* chicken thighs
* Greek yoghurt
* bananas
* toothpaste
* dishwasher tablets

The list should also help prevent duplication.

For example:

“Looks like you may already have rice. Keep it on the list?”

⸻

9.3 Meal planning

PantryPal should allow a household to plan meals for the week.

Meals should have a source, such as:

* home-cooked
* My Food Bag
* leftovers
* ready-made
* takeaway
* eating out
* unknown or flexible

This matters because not every dinner requires a supermarket shop.

The app should first understand what meals are already taken care of before suggesting additional meals.

For example:

“My Food Bag covers Monday to Wednesday, and you are out on Friday. I’ll suggest meals for Thursday, Saturday and Sunday.”

Meal planning should support:

* choosing meals
* accepting suggested meals
* swapping meals
* linking meals to shopping items
* estimating servings
* identifying leftovers
* repeating household favourites

⸻

9.4 Fridge, pantry and freezer

PantryPal should maintain a lightweight view of what the household already has.

This should not become complex inventory management.

The app should support:

* adding items manually
* moving bought items into the kitchen
* marking items as used
* suggesting likely pantry staples
* asking quick confirmation questions
* using fridge and pantry items in meal suggestions
* avoiding unnecessary shopping list items

A useful pattern would be:

“We think you still have oats, rice and soy sauce. Confirm?”

This should be quick to answer and easy to ignore.

⸻

9.5 My Food Bag support

My Food Bag should be treated as a planned meal source.

PantryPal should support:

* marking that My Food Bag is being used this week
* adding My Food Bag meals to the meal plan
* recording the delivery day
* identifying which dinners are already covered
* adding any missing pantry staples to the shopping list
* using My Food Bag meals for one-tap personal food logging
* supporting leftovers from My Food Bag meals

The initial version should not depend on a formal My Food Bag API.

A practical starting point would be:

* manual entry
* screenshot upload
* email/order confirmation import
* recipe card/photo import later

The goal is to make My Food Bag part of the weekly planning picture, not duplicate what it already does.

⸻

9.6 Supermarket specials

PantryPal should be able to use supermarket specials where available.

This may include:

* New World
* Woolworths
* Pak’nSave
* other retailers later

The app should support:

* preferred supermarket selection
* specials-aware meal suggestions
* cheaper substitutions
* price confidence indicators
* store-specific limitations where known

The architecture should not assume that supermarkets provide reliable open APIs.

Specials data may need to come from different sources over time, including:

* public pages
* manual imports
* partner feeds
* receipt history
* future authorised APIs

Because prices and specials can change, the app should not overstate accuracy.

⸻

9.7 Personal food tracking

PantryPal should make food tracking easier for people who want it.

It should not force everyone in the household to track food.

The app should support:

* private food logs
* one-tap logging from planned meals
* portion adjustments
* personal food libraries
* daily summaries
* natural language entry
* reuse of common estimates

For example:

“Log tonight’s My Food Bag chicken meal?”

Options:

* normal portion
* smaller portion
* larger portion
* leftovers
* edit

The app should support approximate calorie tracking without making the experience feel clinical or judgmental.

⸻

10. Initial non-functional requirements

The non-functional requirements are just as important as the features.

⸻

10.1 Usability

PantryPal must be easy to use.

This is not optional.

The app should reduce effort, not create another system the household has to maintain.

Usability expectations:

* adding a shopping item should take only a few seconds
* ticking items off should be instant
* meal planning should be quick
* household members should not need training
* the app should use plain language
* setup should be lightweight
* users should be able to ignore advanced features

A good test is:

“Is this easier than sending a shopping list by text?”

If not, the feature needs to be simplified.

⸻

10.2 Reliability

The shopping list must be reliable.

If the AI recommendation service is unavailable, the shared shopping list should still work.

If specials data is unavailable, meal planning should still work.

If a user has poor connectivity in the supermarket, the active shopping list should still be usable.

Reliability expectations:

* fast list loading
* real-time updates where possible
* offline-tolerant list access
* conflict handling when multiple people update the list
* graceful degradation when external data is unavailable

⸻

10.3 Privacy

Privacy is central to trust.

PantryPal will deal with household behaviour, shopping habits, food preferences, and personal food tracking.

The app should separate shared and private data clearly.

Shared household data may include:

* shopping lists
* meal plans
* kitchen items
* shared household preferences
* My Food Bag meal plans

Private personal data may include:

* food logs
* calorie estimates
* weight-related goals
* symptoms or wellbeing notes
* personal preferences
* personal food library

The default should be:

Shared for household coordination.
Private for personal tracking.

⸻

10.4 Security

PantryPal should apply standard security controls from the start.

Security expectations:

* secure authentication
* household access control
* invite and share-link controls
* encrypted data in transit
* appropriate encryption at rest
* secure handling of uploaded receipts, screenshots and emails
* protection of API keys and integration credentials
* rate limiting and abuse prevention

The security model should be simple enough for users, but strong enough for sensitive personal and household data.

⸻

10.5 Data quality

The product will depend on messy data.

People may type:

* capsicum
* red pepper
* bell pepper

Receipts may use abbreviations.

Recipes may use one unit and supermarkets another.

The app will need a data model that can handle:

* product normalisation
* ingredient matching
* unit conversion
* duplicate detection
* confidence levels
* human correction

Data quality should be improved over time, but the app should not require perfect data to be useful.

⸻

10.6 Integration resilience

External integrations should be treated carefully.

The app may eventually connect with:

* supermarket product and specials data
* My Food Bag emails or account data
* receipt imports
* calendar data
* health or step data
* online carts

But the product should not be dependent on any one external provider.

Integration patterns should allow data sources to be added, removed or replaced without breaking the core app experience.

⸻

10.7 Ethical and safe use

PantryPal should not make unsafe claims.

The app may estimate calories, suggest meals and support dietary preferences, but it should not act as a medical advisor.

It should be careful with:

* allergies
* intolerances
* medical diets
* eating disorders
* weight-loss framing
* children’s food tracking
* health and symptom interpretation

Where needed, the app should use clear disclaimers and encourage professional advice for medical or clinical decisions.

⸻

11. Initial architecture direction

At a high level, PantryPal will likely need the following application areas.

User experience layer

This includes the mobile app and possibly a web app.

The mobile experience is the priority because the app needs to work in the kitchen and supermarket.

Household domain

This manages households, members, roles, shared preferences and permissions.

Shopping list domain

This manages shared lists, list items, categories, quantities, notes, tick-off status and real-time updates.

Meal planning domain

This manages weekly plans, meals, meal sources, ingredients, servings and leftovers.

Kitchen inventory domain

This manages fridge, pantry and freezer items, including confidence around what the household likely has.

Personal tracking domain

This manages private food logs, personal food libraries, portion adjustments and daily summaries.

Product and specials domain

This manages supermarket products, specials, price confidence, store mapping and ingredient-to-product matching.

Integration domain

This handles data coming from outside PantryPal, such as My Food Bag screenshots, receipts, emails, public supermarket data, and future APIs.

AI and recommendation layer

This supports meal suggestions, list generation, substitutions, natural language understanding, food log estimates and explanation of recommendations.

The AI layer should not be the system of record.

Structured application services and databases should hold confirmed household, list, meal and tracking data.

⸻

12. Early conceptual architecture

The early conceptual model is:

Mobile App / Web App
        |
        v
Application API / Backend-for-Frontend
        |
        +-----------------------------+
        |                             |
        v                             v
Shared Household Services       Personal Tracking Services
- Household                     - Food log
- Shopping list                 - Personal food library
- Meal planning                 - Portion adjustment
- Kitchen inventory             - Daily summaries
        |
        v
Recommendation and AI Services
- Meal suggestions
- Shopping list generation
- Substitutions
- Natural language entry
- Preference learning
- Explanation generation
        |
        v
Data and Integration Services
- Product catalogue
- Specials data
- My Food Bag import
- Receipt and email import
- Ingredient matching
        |
        v
External Sources
- Supermarket websites or feeds
- My Food Bag screenshots/emails
- User-uploaded receipts
- Future authorised APIs

The important point is that the core app should remain useful even when the lower integration layer is incomplete.

⸻

13. Early MVP direction

The first version of PantryPal should be deliberately focused.

It should prove that the household experience is useful before trying to solve every integration problem.

The MVP should include:

* household creation
* shared shopping list
* real-time list updates
* basic meal planning
* meal-to-shopping-list generation
* lightweight pantry/fridge items
* manual My Food Bag meal entry
* one-tap personal food logging from planned meals
* personal food library
* basic preferences
* simple export/share list options

The MVP should not depend on:

* direct supermarket APIs
* direct My Food Bag APIs
* exact product pricing
* cart integration
* perfect nutrition data
* barcode scanning
* full pantry inventory
* complex health insights

The first product goal should be:

“Can a household use PantryPal to plan a few meals, create a shared list, avoid buying things they already have, and make food tracking easier?”

If yes, the product has a strong foundation.

⸻

14. Key risks and trade-offs

Supermarket data may be hard to access

There may not be reliable public APIs for supermarket specials, products or cart integration.

The product should avoid depending on unsupported APIs in the early stages.

Pantry tracking can become annoying

If the app asks users to maintain a detailed inventory, they may stop using it.

The product should use light-touch confirmation and useful assumptions.

Food tracking can feel sensitive

Personal eating data is private.

The product must avoid making food tracking feel exposed, judgmental or compulsory.

AI suggestions may be wrong

AI may suggest meals that do not make sense, miss ingredients, or estimate calories poorly.

The product should allow quick correction and should explain assumptions.

Too much scope could slow the MVP

This idea could easily become too large.

The early focus should be shared list, meal plan, My Food Bag support, and easy food logging.

⸻

15. Initial questions to answer next

Before moving into the detailed architecture, the next questions are:

1. Is PantryPal mobile-only at first, or mobile plus web?
2. Should the MVP support only one household per user?
3. What is the minimum useful version of the pantry/fridge feature?
4. How much food tracking should be included in the first version?
5. Should My Food Bag be manual entry first, or should screenshot/email import be included in MVP?
6. Do we want specials in the MVP, or should this be a later feature?
7. How should PantryPal handle privacy between household members?
8. What data should the AI be allowed to use when making suggestions?
9. What should happen when price, product or calorie data is uncertain?
10. What does “super easy to use” mean in measurable terms?

These questions will help shape the first real architecture document.

⸻

16. Recommended next architecture artefact

The next step should be a lightweight application architecture document.

That should include:

* architecture context
* key user journeys
* capability map
* logical application components
* core data entities
* integration approach
* AI usage model
* privacy and consent model
* MVP architecture
* risks, decisions and open questions

The intent is not to over-engineer the product early.

The intent is to create enough structure that PantryPal can be designed, tested and built without losing sight of the practical household problem it is trying to solve.
