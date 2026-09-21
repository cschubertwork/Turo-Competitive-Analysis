# Verification note

Date: 2026-09-22

Every Observed claim in the three full-depth profiles (Mevo, Cityhop, Zilch) was re-checked against the page it cites. A claim passes only where a verbatim quote from the fetched page supports it. A fetch that returned a 404, a paywall, a certificate error, a robots block, or a page with no usable body content is unverifiable; those claims were downgraded to Inferred rather than silently kept. Claims that passed but turned out to be incomplete or slightly wrong were corrected in the profile, not just re-labelled. Wording throughout: claims were re-checked against the pages they cite, not verified true.

- Claims checked: 38
- Passed verbatim: 20
- Downgraded to Inferred (unverifiable source): 13
- Corrected (source loaded, but claim was wrong or incomplete as originally written): 5

## Mevo

**Passed**
- "At its peak it operated across four cities with a mixed fleet including Teslas, Polestars, and Suzuki Swifts." (https://autotalk.co.nz/mevo-enters-voluntary-administration-weeks-after-3-28m-crowdfunding-raise/)
- "The company expanded into Hamilton in 2021 by acquiring Loop from Ebbett Group." (https://autotalk.co.nz/mevo-enters-voluntary-administration-weeks-after-3-28m-crowdfunding-raise/)
- "Mevo has been placed into voluntary administration, just weeks after raising $3.28 million from investors through equity crowdfunding platform Snowball Effect... today (March 30)... The company completed a capital raise that exceeded its $2.2 million target." (https://autotalk.co.nz/mevo-enters-voluntary-administration-weeks-after-3-28m-crowdfunding-raise/)
- "An investor was set to give Mevo $1.7 million which would have seen it through, but... they pulled out because Mevo breached some conditions." (https://www.rnz.co.nz/news/business/591275/mevo-car-sharing-service-goes-into-voluntary-administration)
- "Carbn was founded in July 2020 and works to reduce fleet emission through advisory services and finance solutions." (https://nzbusiness.co.nz/technology/acquisition-targets-low-carbon-fleet-transition)
- "Carbn Group Holdings has acquired the brand and assets of collapsed car-sharing operator Mevo." (https://autotalk.co.nz/carbn-group-acquires-mevo-to-relaunch-wellington-car-sharing/)
- "The acquisition aligns with Carbn Group's existing Zilch network of 20 shared-vehicle electric hubs across New Zealand's major centres." (https://autotalk.co.nz/carbn-group-acquires-mevo-to-relaunch-wellington-car-sharing/)
- "The Wellington relaunch will feature a fleet of Suzuki Swifts operating under the Mevo brand... plans for national expansion and a broader range of electric vehicle types as the business develops." (https://autotalk.co.nz/carbn-group-acquires-mevo-to-relaunch-wellington-car-sharing/)
- Current homepage confirms operation in Wellington and Queenstown only. (https://mevo.co.nz/)
- "The partnership offers AA members up to $100 in free Mevo credit in their first year," covering Auckland, Wellington, and Hamilton. (https://autotalk.co.nz/car-share-operator-mevo-joins-forces-with-the-automobile-association/)
- "The fleet is owned and maintained by Mevo and powered by Meridian." (https://www.meridianenergy.co.nz/ev/mevo)
- Headline and opening paragraph describe Mevo as "Wellington car-sharing king" ahead of its Auckland launch. (https://www.nzherald.co.nz/business/companies/freight-logistics/new-at-policy-sees-wellington-car-sharing-king-mevo-hit-go-for-auckland-launch/KN5VOZHI5AJQBZVKQUEKWMOIZ4/)
- The same article confirms the Auckland Transport policy change "authoriz[ed] 'free-floating' car-share models" for Mevo. (https://www.nzherald.co.nz/business/companies/freight-logistics/new-at-policy-sees-wellington-car-sharing-king-mevo-hit-go-for-auckland-launch/KN5VOZHI5AJQBZVKQUEKWMOIZ4/)
- "Right now, we have fifteen plug-in hybrid Audi A3 e-trons around Wellington CBD and at Wellington International Airport." (https://thespinoff.co.nz/business/14-03-2018/the-primer-the-car-sharing-service-putting-electric-vehicles-on-wellingtons-roads)
- Current Wellington pricing page confirms three tiers (Compact $19/hr-$95/day, Comfort $22/hr-$110/day, Premium $25/hr-$125/day), "First 100km each trip is free" at $0.39/km beyond, and "Charging, parking, and insurance are always included." (https://mevo.co.nz/wellington/pricing)

**Downgraded to Inferred (unverifiable on 2026-09-22)**
- Mevo founded 2014 by Erik Zydervelt and Finn Lawrence, launched late 2016 with Audi A3 e-tron: mevo.co.nz/mission loaded but contained no founding date, founder names, or vehicle model.
- Nelson lost its only car-sharing service after Mevo's exit: thepress.co.nz returned only a page header with no body content; business.scoop.co.nz and auckland.scoop.co.nz both returned 403.
- Standard insurance excess of $4,000, Standard/Enhanced/Total Cover tiers, weekly add-on to $0: support.mevo.co.nz returned a TLS certificate mismatch (the help site is Intercom-hosted and the fetch could not validate the certificate).
- Wellington City Council "Home Zone" cost-neutral parking arrangement: the cited AA-partnership article was fetched successfully but contains no mention of a Home Zone or council parking deal.
- Z Energy held up to a 32% stake in pre-collapse Mevo: not fetched against a primary source in this pass.
- Carbn Group is Auckland-based: the nzbusiness.co.nz article that confirmed Carbn's July 2020 founding date does not state a location.
- Suzuki Swift charged at $1/minute up to a $20/hour rate after ~20 minutes: support.mevo.co.nz returned the same certificate error as above; superseded in the profile by the verified three-tier pricing.

**Corrected (source loaded, original claim was wrong or overstated)**
- Removed the claim that Mevo's pre-collapse fleet was marketed as "New Zealand's first electric-hybrid car share" and that vehicles were "parked on-street": the Spinoff article confirms the fifteen-vehicle Audi A3 e-tron fleet and its two locations, but not the superlative or the parking detail.
- Removed a secondary description of Carbn Group as a "car-share rival" of Mevo prior to acquisition: the cited businessdesk.co.nz article returned HTTP 402 (paywalled) and no alternative fetched source confirmed the phrase.
- Corrected Wellington pricing from an earlier draft figure of "50km included" to the verified "first 100km free, then $0.39/km."

## Cityhop

**Passed**
- Full Wikipedia article confirms: founded Auckland 2007 by Victoria Carter with Jucy Rentals; launched by PM Helen Clark with three vehicles; Toyota New Zealand acquisition November 2018; operation in Auckland, Wellington, Christchurch; membership and fleet growth from ~6,000 members/120 vehicles (2019) to 10,000+ members/150+ vehicles (2020). (https://en.wikipedia.org/wiki/Cityhop)
- Full cityhop.co.nz/rates page confirms the Hop Starter (free) and Hop Regular ($10/month, 3-month minimum) plans, the per-vehicle hourly/daily rates, and the "$0.59 per km" excess-kilometre charge past 150km. (https://www.cityhop.co.nz/rates)
- Toyota Financial Services CEO Brent Knight: "Our goal is to help Cityhop grow and offer more people a wider range of transport alternatives." (https://autotalk.co.nz/toyota-financial-services-announces-partnership-cityhop/)
- Cityhop founder Victoria Carter: "This partnership provides a massive opportunity to accelerate growth in our existing markets." (https://autotalk.co.nz/toyota-financial-services-announces-partnership-cityhop/)

**Downgraded to Inferred (unverifiable on 2026-09-22)**
- Standard Liability excess of $2,000/$2,500 by vehicle class: support.cityhop.co.nz returned 403.
- Reduced Liability cover at $4.50/hour (capped $27/day) reducing excess to $750: support.cityhop.co.nz returned 403.
- 8 employees as of a 1 July 2024 filing: sourced only to a company-data aggregator via search, never fetched directly.
- Z Energy parking partnership at service stations: not fetched against a primary source in this pass.

**Corrected**
- Removed a quoted line attributed to Toyota NZ ("a shared mission to help create more accessible cities...") that does not appear in the cited drivencarguide.co.nz article; kept the underlying acquisition timing, which the article does support.

## Zilch (formerly Yoogo Share)

**Passed**
- Metropol article on the Christchurch launch confirms March 2018 timing and named figures: Yoogo Share general manager Kirsten Corson, Christchurch City Council resource efficiency manager Kevin Crutchley, and Christchurch Mayor Lianne Dalziel. No mention of the Prime Minister. (https://metropol.co.nz/electric-car-sharing-scheme-yoogo-share-launches-in-christchurch/)
- "Electric car sharing service Yoogo Share has relaunched as Zilch," plus "more than 2000 bookings monthly in Christchurch" and "saved about 240 tonnes of carbon in the city." (https://autotalk.co.nz/yoogo-share-rebrands-as-zilch/)
- "Carbn, has acquired electric mobility company Zilch, with the move to help Kiwi businesses reimagine how they manage their transportation," including that Zilch "was launched in Christchurch in 2018 with EV Public car sharing" and "expanded in 2020... using specialist tech and service which they call eMaaS." (https://www.scoop.co.nz/stories/BU2312/S00062/zilch-acquired-by-carbn-acquisition-to-accelerate-nzs-low-carbon-fleet-transition.htm)
- Full zilch.nz/about page confirms: 5 cities, 17 hubs, the "same fleet philosophy, different lengths of time" framing against Mevo, 165,770+ trips, 1.4M+ kg CO2 saved, Sustainable Transport and Westpac Innovation awards, and the brand line "A car when you need one. Nothing when you don't." (https://www.zilch.nz/about/)
- "Only pay for the time a car is in use. Staff book by the hour or day with no lease commitments, no fixed monthly cost, no vehicles sitting idle between trips." (https://www.zilch.nz/business/)
- Subscription pricing page confirms per-km charging and "a discounted 500 KM per week for $50" prebuy package. (https://www.zilch.nz/24-7-subscriptions-2/)

**Downgraded to Inferred (unverifiable on 2026-09-22)**
- 8 hubs and 100 EVs at Yoogo Share's original launch, plus the named foundation-member list: driveelectric.org.nz returned 404.
- Genesis Energy paid $2 million for a 40% stake: genesisenergy.co.nz returned only a headline with no body content; nzi.co.nz (an alternate source for the same figure) returned 403.
- Carbn Group and PowerFinance strategic partnership: not fetched against a primary source in this pass.
- Zilch's Heart of the City Auckland business-directory listing: not fetched against a primary source in this pass.

**Corrected**
- Replaced "launched February 2018... Prime Minister Jacinda Ardern officiating" with the verified March 2018 date and the actually-named officials (no PM involvement found).
- Replaced "personal subscriptions from $99/week... $50-$200 for 625-2,500km/month, $0.50/km overage" with the figures the fetched pricing page actually shows: per-km billing plus a $50/500km-per-week prebuy package. The $99/week figure could not be reproduced against the live page and may be stale.
- Split a single claim that conflated the Yoogo-to-Zilch rebrand with the Carbn Group acquisition into two correctly sequenced and separately sourced claims: the rebrand (autotalk.co.nz, undated relative to the acquisition) happened before Carbn's December 2023 acquisition of the already-renamed Zilch (scoop.co.nz).
