# Phase 1 Problem Discovery: Finance Ops, Procurement, Vendor/Contract Ops, B2B Commerce, Revenue Leakage

Date: 2026-10-05. Analyst notes up front:

- **Source quality.** URLs below come from live web search results in this session. A few of the cited pages are vendor blogs or SEO/AI content farms (stealthagents.com, digiparser.com, beri.net, redresscompliance.com, cloudnuro.ai). Their statistics are labeled **[low-confidence source]** and should be checked against primary data before anyone relies on them.
- **What could not be checked.** Outbound page fetches were blocked by the egress proxy (mondaq, clm.com, thenextweb, enable.com), and the search budget ran out late in the session. Funding figures marked **(verify)** come from analyst background knowledge and were not confirmed in this session.
- **Pain estimates.** Dollar figures are order-of-magnitude estimates with the reasoning shown. They are not measured.

---

## 1. IEEPA tariff refund pass-through: who keeps the refund (importer vs. B2B customers)

- **Problem:** The Supreme Court voided the IEEPA tariffs on Feb 20, 2026. Mid-market and enterprise importers now get refunds through CBP's CAPE portal. Many of them passed the tariffs on to B2B customers as surcharges or price increases, so neither side has an entry-level, invoice-level record of who actually paid what, and that record is what every claim, counter-claim and settlement depends on.
- **Who has it:** Two sides. (a) Controllers, trade compliance staff and GCs at importers who received refund requests. (b) Procurement and AP at the downstream B2B buyers who paid the surcharges. More than 330,000 importers filed 53M+ entries with IEEPA duties, and the number of downstream buyers is several times that.
- **Evidence:**
  - KPMG/EY: CBP built the CAPE module, and claims are CSV lists of entry summaries. The scale: "more than 330,000 importers made more than 53m entries with IEEPA duties." (https://kpmg.com/us/en/taxnewsflash/news/2026/03/us-cbp-ieepa-duty-refund-process-update.html, https://globaltaxnews.ey.com/news/2026-0586)
  - Mondaq: "The most significant disputes associated with IEEPA refunds may no longer involve the government, but instead … customers, suppliers, distributors…" (https://www.mondaq.com/unitedstates/export-controls-trade-investment-sanctions/1807886/what-every-multinational-should-know-about-the-emerging-battle-over-who-ultimately-keeps-ieepa-tariffs)
  - Class actions were filed against FedEx and UPS over itemized IEEPA duty charges (https://www.fortune.com/2026/03/13/americans-demanding-tariff-refunds-suing-costco-fedex).
  - Law firms are publishing guides for suppliers who are fielding customer refund requests (https://www.agg.com/news-insights/publications/practical-guidance-for-suppliers-fielding-customer-tariff-refund-requests/).
  - Total at stake is roughly $130-175B (https://www.dickinson-wright.com/news-alerts/client-alert-tariff-alert).
- **Economic pain:** A $500M-revenue distributor that paid $10M+ in IEEPA duties and passed on 50-90% of it faces $5-9M of contested money and hundreds of customer requests. A buyer that absorbed $2M of surcharges across 200 suppliers is leaving money unclaimed. Recoverable value per company runs $100K to $10M+.
- **Existing solutions:** Customs brokers and Big 4/law firms handle the government side. Caspian ($5.4M seed) and Pax AI ($4.5M seed) work on drawback and duty recovery. **No product reconstructs surcharge pass-through and handles the B2B claims on either side.**
- **Why now / why unsolved:** The problem only appeared in Feb-Apr 2026. The data is scattered across ACE entries, ERP invoices, surcharge line items and price-increase letters, which is a good job for LLMs.
- **Risk:** This is a one-time windfall event. Unless the product expands into ongoing tariff and surcharge management, it is a services business with a 12-24 month window.
- **Verdict: MEDIUM.** The pain is enormous and urgent, and the wedge is excellent for fast pilots and contingency-fee revenue. It becomes STRONG only if it expands into #2 and #3.

## 2. Supplier surcharges and price increases (tariff, fuel, index-linked) billed without validation against contract

- **Problem:** Since 2025, suppliers have added tariff surcharges, fuel surcharges and "cost-justified" price increases as invoice line items. AP pays them because nobody checks them against the contract's escalation clause, the underlying index or the actual duty rate. Many of these surcharges should now reverse after the IEEPA ruling and are not reversing.
- **Who has it:** CPOs, AP managers and category managers at manufacturers, distributors, retailers, hospitals (non-clinical spend) and local governments. Roughly 40K+ US companies with more than $100M in spend.
- **Evidence:**
  - A Dutchess County (NY) comptroller memo: vendors have begun adding tariff-related surcharges to invoices submitted for payment, and some surcharges are percentage-based and could grow (https://www.dutchessny.gov/Departments/Comptroller/Docs/251023-Tariff-Charge-Memo.pdf).
  - A Mitsubishi Chemical 10% tariff surcharge letter (https://www.abcsupply.com/wp-content/uploads/price-increase-announcements/Mitsubishi%20Chemical%20Group%20Tariff%20Surcharge%20Letter%207.1.25.pdf).
- **Economic pain:** If 2-5% of direct spend is now under surcharge or escalation, and 10-30% of that is unjustified or failed to reverse, a $1B-spend manufacturer loses $2-15M a year.
- **Existing solutions:** Coupa, SAP Ariba and Zip check PO vs. invoice vs. receipt, but they match against the PO price, which already includes the increase. Post-payment recovery auditors (PRGX, private) work contingency years after the fact. Rivvun AI ($7.55M seed, Jun 2026) targets buy-side contract compliance broadly (https://dealroom.co/news/134334-rivvun-ai-raises-7-55m-seed-to-recover-money-enterprises-lose-between-co/).
- **Why now:** Tariff volatility (Section 232 at 50%, then the IEEPA reversal) plus LLMs that can read contract clauses and price-increase letters.
- **Verdict: STRONG.** "AI that checks every supplier price increase against your contract and the real index" is easy to explain, has hard ROI, and can run on AP data in a 2-week pilot.

## 3. Buy-side contract terms not enforced (rebates, volume tiers, MFN, SLA credits, price holds)

- **Problem:** Enterprises negotiate rebates, tiered pricing, price holds, MFN clauses and service credits, then never monitor them. The terms sit in PDFs inside a CLM while invoices flow through the ERP with no link between the two.
- **Who has it:** CPOs and procurement ops at companies with $250M+ in third-party spend. Roughly 15K globally.
- **Evidence:**
  - Rivvun AI, founded by Icertis veterans: "enterprise procurement functions lose up to a third of planned savings during execution, with an additional 3–4% of total external spend lost to inefficiency and non-compliance." It estimates "$2 trillion" a year goes unrecovered between obligation and settlement (https://aimagazine.com/globenewswire/3309729, https://itbrief.co.uk/story/rivvun-ai-raises-usd-7-55m-seed-round-led-by-sitara).
  - Enable: distributors typically miss "4% of their rebate revenue" (https://enable.com/blog/the-supplier-rebate-model-is-broken-and-its-costing-distributors).
- **Economic pain:** 1% of $1B in spend is $10M a year. Even a 0.3% recovery gives $3M, enough to support a $150K+ ACV.
- **Existing solutions:** Enable (rebates, $120M Series D at a $1.12B valuation, 2023: https://tech.eu/2023/11/10/uk-founded-enable-secures-120m-for-rebate-management-now-valued-at-1-12b). Icertis, Ironclad and Sirion (CLM, which store contracts but don't enforce them). Rivvun AI (seed). Recovery audit firms.
- **Why unsolved:** CLM and P2P have always been separate systems. Mapping a clause to the right invoice lines used to need humans, and LLMs make it tractable now.
- **Verdict: STRONG.** This is the core "contract-to-cash enforcement layer" thesis. It is getting crowded early (Rivvun, CLM vendors adding AI), so the edge has to come from data integration and recovery execution.

## 4. Sell-side revenue leakage: price escalators, minimums, overages and true-ups never invoiced

- **Problem:** B2B sellers with complex contracts (annual CPI escalators, committed minimums, overage tiers, ramp deals) routinely fail to invoice what the contract allows. Terms live in Salesforce or PDF while billing runs from a separate config.
- **Who has it:** CFOs, RevOps and billing ops at SaaS, IT services, logistics, B2B data/API and industrial service companies with more than 500 enterprise contracts. Roughly 20K+ companies.
- **Evidence:**
  - Orb blog: SaaS companies lose "3-5% of ARR," and usage-based models see "4-9%" leakage (https://www.withorb.com/blog/revenue-leakage-statistics) [vendor source].
  - Fintel stat (via search): 73% of SaaS finance teams cannot quantify their leakage.
  - Rivvun's "Margin Defence" agent targets the same gap (https://dealroom.co/news/134334-rivvun-ai-raises-7-55m-seed-to-recover-money-enterprises-lose-between-co/).
- **Economic pain:** 1-3% of a $200M revenue base is $2-6M a year. The money is recovered at near-100% margin.
- **Existing solutions:** Billing platforms (Zuora, Metronome, Orb, Chargebee) only bill what they are configured to bill. CPQ and CLM. Rivvun. MGI/Zenskar-type contract-to-invoice tools.
- **Why now:** The move to usage, credit and hybrid AI pricing multiplies contract complexity. LLM contract extraction makes the audit automatable.
- **Verdict: STRONG.** "We find the money your contracts say customers owe you" sells itself with self-funding ROI. The overlap with #3 suggests one platform could serve both sides.

## 5. AI/LLM token and agent spend: allocation, chargeback, forecasting and budget overruns

- **Problem:** Enterprises cannot attribute or forecast their exploding AI spend: API tokens, coding agents, credits embedded in SaaS, and agent workflows. Finance can't charge it back to teams, products or customers, and budgets are blown mid-year.
- **Who has it:** CFOs, FP&A, FinOps and engineering leaders at every company spending more than $500K a year on AI. Roughly 10-20K companies and growing fast.
- **Evidence:**
  - "Uber burned its entire 2026 AI coding budget in about four months and capped engineers at $1,500/month" (https://getunblocked.com/blog/finops-for-ai-coding/).
  - The FinOps Foundation's State of FinOps 2026 says 98% of teams manage AI spend and token cost management is the top challenge (https://www.finout.io/blog/finops-for-ai-tokens-why-the-rules-changed-and-what-to-do-about-it).
  - Ramp AI Index: the top 1% of adopters spend more than $7,400 per employee per month on AI (https://ramp.com/leading-indicators/ai-index-june-2026).
  - "Only about 20% forecast AI spend within ±10%" (FinOps survey, cited at https://briefglance.com/articles/the-ai-bill-shock-why-consumption-pricing-is-breaking-corporate-budgets) [secondary].
- **Economic pain:** A company spending $10M a year on AI typically wastes 20-30% (wrong model, runaway agents, idle seats), so $2-3M a year, plus the chargeback work.
- **Existing solutions:** Cloud FinOps vendors adding AI modules: Vantage, CloudZero, Finout. Gateways and observability: Portkey, Helicone, LiteLLM, OpenRouter. Ramp and Brex for card-level spend. Several seed-stage AI-cost startups.
- **Why unsolved:** Spend is fragmented across API keys, SaaS credits, card spend and cloud marketplaces, each with incompatible units (FOCUS v1.4 only just added AI). There is no system of record linking "agent X did task Y for customer Z at cost $C."
- **Verdict: STRONG.** This is the clearest "where the world is going" story. The risks are crowding and that Ramp, Datadog or cloud providers bundle it, so the wedge has to be unit economics per agent and per customer (COGS for AI products), not dashboards.

## 6. SaaS spend shifting from seats to consumption and credits, unmanageable by seat-based SaaS management tools

- **Problem:** SaaS vendors have shifted to credits and consumption (Salesforce Agentforce, Microsoft Copilot credits, Atlassian, HubSpot). Buyers' SaaS management tools, built around seat counts and renewals, can't verify usage invoices, compare credit "currencies" or catch overages.
- **Who has it:** IT procurement, SaaS ops and FP&A at companies with more than 500 employees. Roughly 50K+ companies.
- **Evidence:**
  - CloudEagle: "85% of SaaS vendors now charge by consumption and most enterprises aren't ready" (https://www.cloudeagle.ai/newsroom/85-of-saas-vendors-now-charge-by-consumption-and-most-enterprises-arent-ready) [vendor].
  - Month-to-month swings of 40%+ are common in AI-heavy SaaS spend, citing Ramp April 2026 data (https://briefglance.com/articles/the-ai-bill-shock-why-consumption-pricing-is-breaking-corporate-budgets) [secondary].
  - Seven vendors bill AI as credits, and no two credit currencies are comparable (https://redresscompliance.com/enterprise-ai-credits-pricing-compared-pillar-2026) [low-confidence source].
- **Economic pain:** Overages and unused prepaid credits of 10-25% on $5-50M of SaaS spend come to $0.5-5M a year.
- **Existing solutions:** Zylo, Productiv, CloudEagle, Torii, Vendr, Tropic, Vertice, Spendflo. All of them are seat- and renewal-centric.
- **Why now:** The pricing model transition is happening during 2025-2027.
- **Verdict: MEDIUM.** The pain is real, but incumbents will add the features. It is best folded into #5 as one "consumption spend control" platform.

## 7. Software license audits and true-ups (Broadcom/VMware, Oracle Java, Microsoft, SAP)

- **Problem:** Vendors use license audits as a revenue lever. Enterprises can't produce defensible entitlement-vs-deployment positions quickly and end up paying seven-figure true-ups.
- **Who has it:** CIOs, IT asset managers and procurement at companies with more than 1,000 employees. Roughly 20K in the US.
- **Evidence:**
  - Vendor audits rose from 40% to 62% of companies in 2024, and 32% paid over $1M (https://block64.com/blog/the-software-audit-surge-why-62-of-companies-faced-vendor-audits-in-2024).
  - Broadcom is the most active auditor, named by 33% of enterprises (https://www.dbta.com/Editorial/Trends-and-Applications/RESEARCH-at-DBTA-Survey-Software-Licensing-Audits-on-the-Rise-Exacerbated-by-the-Cloud-169131.aspx).
- **Economic pain:** $1-10M per audit event, plus the consultant fees.
- **Existing solutions:** Flexera, Snow (now part of Flexera), ServiceNow SAM, Licenseware, and licensing consultancies (Redress, etc.).
- **Why unsolved:** Entitlement data lives in contracts and order forms, deployment data lives in IT tools, and the rules are byzantine. LLMs can now read the licensing contracts.
- **Verdict: MEDIUM.** The dollars are high and the problem is acute, but buyers are IT asset managers with long sales cycles, and it is a legacy-dominated category.

## 8. Retail and CPG deductions (chargebacks, OTIF fines, short-pays)

- **Problem:** CPG and consumer brands lose 1-5% of gross sales to retailer and distributor deductions (Walmart, Target, KeHE, UNFI). Many of them are invalid, and disputing them means manually pulling PODs, BOLs and promo agreements from portals.
- **Who has it:** AR, deductions analysts and controllers at CPG, food & bev, consumer goods, and industrial suppliers to big-box. Roughly 30K+ brands in the US.
- **Evidence:**
  - Glimpse ($10M Series A, 8VC/YC): deductions can wipe out "10% to 30% of profit margins," and disputes mean "pulling invoices, cross-referencing spreadsheets, and emailing retailers" (https://foodindustryexecutive.com/2025/04/glimpse-secures-10m-to-automate-deduction-management-for-cpg-brands/).
  - Walmart has 75 AP deduction codes (https://www.8thandwalton.com/blog/walmart-deduction-codes?hsLang=en).
- **Economic pain:** A $200M brand with 3% deductions has $6M deducted. If 20-40% of that is invalid and recoverable, the prize is $1-2M a year.
- **Existing solutions:** Glimpse ($10M A; a16z also invested), SupplyPike, Carbon6, HighRadius deductions, Vividly/Promomash for trade promotion, iTradeNetwork.
- **Why now:** Agents can now log into retailer portals and assemble dispute packets.
- **Verdict: MEDIUM.** The pain is proven and the ROI is clear, but ACV is often under $50K for mid-market brands and the space is getting crowded. Upside comes from expanding to manufacturing and distribution deductions.

## 9. Freight and parcel invoice errors (accessorials, rate mismatches, duplicate billing)

- **Problem:** 3-10% of freight invoices contain errors, mostly in accessorials. Mid-market shippers can't audit LTL, ocean, drayage and parcel invoices against contracted rates and tenders.
- **Who has it:** Logistics, transportation and AP at shippers with $10M+ in freight spend. Roughly 25K US companies.
- **Evidence:**
  - "5% to 15% of all commercial freight invoices contain carrier billing errors—costing mid-market shippers up to 7%" (https://gingercontrol.com/blog/freight-invoice-audit-guide) [vendor].
  - Portcast is building AI freight audit (https://www.portcast.io/blog/portcast-joins-google-ai-first-startups-program-driving-the-next-phase-in-ai-powered-freight-audit-2).
- **Economic pain:** 2-5% of $50M in freight is $1-2.5M a year.
- **Existing solutions:** Cass Information Systems, Trax, nVision, Intelligent Audit, CTSI; parcel audit firms (refund-retrieval); Loop (AI freight audit, a16z-backed, verify).
- **Why unsolved:** Freight audit and payment (FAP) is mature and services-heavy. AI wins on ocean, drayage and accessorials.
- **Verdict: WEAK-MEDIUM.** The money is real but the category is old and contested (Loop and others). Not category-defining.

## 10. Duplicate and erroneous payments in AP

- **Problem:** Even with AP automation, 0.8-2% of disbursements go out as duplicate or erroneous payments. Causes include vendor master duplicates, invoice number variants and multiple ERPs.
- **Who has it:** AP and internal audit at companies with more than $500M in revenue. Roughly 15K.
- **Evidence:** APQC Open Standards Benchmarking: top performers lose about 0.8% of disbursements to duplicates and erroneous payments, the median 1.5%, and bottom performers 2.0% (cited at https://digiparser.com/statistics/accounts-payable-error-rate [low-confidence source]; also https://www.corpay.com/en-NZ/resources/blog/duplicate-payment).
- **Economic pain:** Even 0.1% of $1B in disbursements is $1M a year. The 1.5% figure is likely inflated by error definitions.
- **Existing solutions:** AppZen, Oversight, PRGX recovery audit, SAP and Coupa native checks, plus many AP automation vendors (Stampli, Tipalti, Bill).
- **Verdict: WEAK.** It's a feature, not a company, and the market is saturated. Fold it into #3 or #11.

## 11. Vendor bank-account-change fraud and BEC in AP

- **Problem:** Fraudsters impersonate suppliers and request bank account changes, and AP teams verify by phone and email (or not at all). Deepfake voice and AI-written emails now make this worse.
- **Who has it:** AP, treasury and the CISO at every mid-market and enterprise company. Roughly 100K+.
- **Evidence:** AFP 2025 Payments Fraud Survey: BEC at 63% of orgs, and vendor impersonation rose to 45% from 34%. The AFP 2026 report says 74% were affected by BEC in 2025 (https://www.corpay.com/resources/blog/business-email-compromise-ap).
- **Economic pain:** Single losses of $100K-$5M. Expected loss and insurance cost run $200K-$1M a year for a mid-market company.
- **Existing solutions:** Trustpair, Eftsure, Paymode-X/Bottomline, Nacha account validation, Coupa/Tipalti supplier portals, and email security (Abnormal Security, $5B+ valuation).
- **Why now:** GenAI deepfakes.
- **Verdict: MEDIUM.** The pain is huge but buyers see it as a security feature, and funded players already exist (Trustpair, Eftsure). A "verified supplier identity network" could be a network-effects play, but distribution is hard.

## 12. Cash application and remittance matching

- **Problem:** B2B payments arrive with remittance detail separated (emails, PDFs, AP portals, lockbox), so AR analysts spend 10-15 hours a week manually matching payments to invoices.
- **Who has it:** AR and shared services at B2B companies with $50M+ in revenue. Roughly 60K.
- **Evidence:** "Manual cash application consumes 10 to 15 hours per analyst every week, according to NACM research" (https://www.stuut.ai/blog/risks-manual-cash-application) [vendor].
- **Economic pain:** 2-10 FTEs, or $150K-$1M a year, plus the DSO impact.
- **Existing solutions:** HighRadius ($3.1B valuation, 2021, verify), Billtrust (EQT, verify), Versapay, Esker, Stuut (a16z Series A, verify), Fazeshift (YC, $4M A May 2026), Centime, Bill.
- **Verdict: WEAK.** Crowded and solved enough. AI agents are already the default pitch.

## 13. B2B collections across AP portals (Ariba, Coupa, Tungsten) and dispute handling

- **Problem:** Large customers force suppliers to submit invoices through dozens of AP portals, each with its own login and rules. Invoices get rejected for format issues, and collectors chase status by hand, which inflates DSO.
- **Who has it:** AR and collections at suppliers selling to enterprises (IT services, manufacturing, staffing). Roughly 40K.
- **Evidence:** Remittances "are typically sent via emails, EDI or hosted in AP portals," which complicates matching (https://www.esker.com/en-au/blog/order-cash/cash-application-what-it-why-it-matters-how-secure-revenue-faster-ai-powered). Practitioner pain is well known, but no high-quality survey was retrieved this session.
- **Economic pain:** 5-15 days of excess DSO on $500M in revenue is $7-20M in working capital, plus FTEs.
- **Existing solutions:** Monto, Tesorio, HighRadius, Billtrust, Versapay, Esker, Upflow, and Kolleno (smaller).
- **Why now:** Browser agents can operate portals at scale.
- **Verdict: MEDIUM.** A good agentic wedge, but it is becoming a feature of AR suites.

## 14. Intercompany reconciliation and close for multi-entity companies

- **Problem:** Multi-entity companies spend days every close resolving intercompany mismatches (timing, FX, missing counterpart entries) across ERPs before eliminations can run.
- **Who has it:** Controllers at multinationals and PE roll-ups with 10+ entities. Roughly 25K globally.
- **Evidence:**
  - "Organizations with 10 or more legal entities spend an average of 4.3 days per financial close cycle resolving intercompany mismatches" (attributed to Deloitte via https://stealthagents.com/research/ai-intercompany-reconciliation-automation-statistics-2026 [low-confidence source]).
  - BlackLine on year-end intercompany pain (https://www.blackline.com/blog/easing-the-pain-of-the-intercompany-year-end-close/).
  - Dimensional Research (2023): 99% report challenges.
- **Economic pain:** 3-10 FTEs plus audit adjustments, or $0.5-2M a year at enterprises.
- **Existing solutions:** BlackLine, Trintech, OneStream, SAP ICR, FloQast, Numeric, plus AI-native ERPs (Rillet, $1B valuation Aug 2026; Campfire; DualEntry) that eliminate the problem for new companies.
- **Verdict: WEAK-MEDIUM.** The pain is real but the category is incumbent-dominated, and AI-native ERPs will absorb it.

## 15. Revenue recognition for usage, credit and hybrid pricing (ASC 606), especially at AI companies

- **Problem:** AI and usage-priced companies sell prepaid credits, commits with overage and token bundles. Finance does variable consideration, breakage and reallocation in spreadsheets, and auditors push back.
- **Who has it:** Controllers and revenue accountants at SaaS/AI companies with $20M-1B in ARR. Roughly 10K.
- **Evidence:** "When 30% of prepaid annual credits go unused, finance teams face challenges recognising breakage," and companies are "often reconciling spreadsheets manually, which isn't scalable at $50M ARR" (https://www.zenskar.com/finance-glossary/credit-breakage, https://www.aprio.com/insights-events/revenue-recognition-for-ai-companies-asc-606-tokens-tax-ins-article-tech/).
- **Economic pain:** 2-5 FTEs, audit fees and restatement risk: $300K-$1.5M a year.
- **Existing solutions:** Zuora RevPro, NetSuite ARM, Leapfin, RightRev, Tabs (AI billing and revrec, funded, verify), Rillet (native revrec), Metronome/Orb for billing.
- **Verdict: MEDIUM.** The problem is real and growing with AI pricing, but Rillet and other AI-native ERPs bundle it. Better as a feature than a standalone category.

## 16. Usage-billing errors on the buy side: nobody verifies vendors' metered invoices

- **Problem:** As more inputs are metered (cloud, AI APIs, data vendors, telecom, payments processing fees, logistics), buyers pay usage invoices they can't independently verify against their own telemetry or contract rate cards.
- **Who has it:** FP&A, FinOps and AP at tech-forward mid-market and enterprise companies. Roughly 20K.
- **Evidence:** Sell-side data shows metering errors cause 1-3% leakage (https://www.withorb.com/blog/invoice-accuracy-billing-error-statistics) [vendor]. If sellers miscount, buyers are overbilled too. Payment processing fee audits (interchange optimization) are a known recovery niche.
- **Economic pain:** 1-3% of $20M in metered spend is $200-600K a year.
- **Existing solutions:** Fragmented. Cloud FinOps covers cloud only, and payment fee auditors cover processing only.
- **Verdict: MEDIUM.** Conceptually strong ("an auditor for every metered bill"), but each meter needs its own integration. It fits as a module of #5.

## 17. Cloud commit (EDP/MACC/GCP) shortfall and marketplace burn-down optimization

- **Problem:** Enterprises sign multi-year cloud commits 15-40% above realistic consumption to get discount tiers, then face shortfall liability or scramble to burn the commit through marketplace purchases.
- **Who has it:** FinOps, procurement and CFOs at companies with $5M+ in annual cloud spend. Roughly 8K.
- **Evidence:** Shortfall liability runs 10-20% of commitment value, and in 21 of 30 EDP deals reviewed, buyers committed 20-40% above realistic consumption (https://redresscompliance.com/aws-edp-shortfall-risk-management) [consultant, low-confidence source]. WM Technology's 10-Q discusses cloud commitments (https://www.sec.gov/Archives/edgar/data/1779474/000177947425000035/maps-20250630.htm).
- **Economic pain:** 10% of a $10M commit is $1M a year.
- **Existing solutions:** ProsperOps, Vantage, CloudZero, Spot (NetApp), Tackle/Clazar (marketplace), and consultants.
- **Verdict: WEAK.** Mature FinOps territory with a narrow buyer base.

## 18. SaaS auto-renewals missed and termination windows lost

- **Problem:** Companies miss 30-90-day cancellation and renegotiation windows buried in MSAs, so unwanted renewals and uplifts auto-renew.
- **Who has it:** IT, procurement and finance at companies with 200+ employees.
- **Evidence:** Vendr: missing cancellation deadlines is widespread (https://www.vendr.com/blog/saas-renewal-best-practices-missed-cancellation). Flexera on mishandled auto-renewals (https://www.flexera.com/blog/saas-management/how-to-mishandle-a-saas-auto-renewal-contract/).
- **Economic pain:** $50-500K a year at mid-market companies.
- **Existing solutions:** Vendr, Tropic, Zylo, Spendflo, Vertice, Ramp (contract tracking built in), and every CLM.
- **Verdict: WEAK.** Commoditized, and Ramp, Brex and Zip give it away.

## 19. Procurement intake and orchestration

- **Problem:** Employees don't know how to buy. Requests bounce between legal, security, IT and finance through email and Slack.
- **Who has it:** Procurement at companies with more than 1,000 employees.
- **Evidence:** Zip raised a $190M Series D at a $2.2B valuation, with 2025 revenue of $193M (https://ziphq.com/blog/series-d, https://getlatka.com/companies/zip).
- **Existing solutions:** Zip, Tropic, Omnea, Levelpath, Coupa, Ariba, Ramp Procurement.
- **Verdict: WEAK** as a new wedge. Zip already defines the category, so the gap is execution, not problem discovery.

## 20. Supplier onboarding and vendor master data quality

- **Problem:** Onboarding a supplier takes 2-8 weeks of forms, W-9/tax, bank, insurance, security and ESG checks, and vendor master files end up 20-30% erroneous or duplicated, which feeds duplicate payments and fraud (#10, #11).
- **Who has it:** Procurement ops and AP at enterprises, manufacturers and hospitals (non-clinical). Roughly 30K.
- **Evidence:**
  - Average onboarding of 18.8 days, ranging up to 91+ days. Master files carry a 20-30% error and duplicate rate (https://stealthagents.com/research/vendor-onboarding-cycle-time-statistics-2026 [low-confidence source]).
  - The APQC median for system setup is 3 days (same source).
  - Graphite 2026 Supplier Data Benchmark: 47% have neutral-or-lower confidence in their supplier data (https://www.graphiteconnect.com/2026-supplier-data-report).
- **Existing solutions:** Graphite Connect (funded), HICX, Coupa Supplier Portal, Tealbook, Certa, TealBook data.
- **Verdict: MEDIUM.** A shared "verified supplier network" has network effects, but it is a slow sale and funded incumbents exist.

## 21. E-invoicing mandates (Belgium Jan 2026, Poland KSeF Feb 2026, France Sep 2026, Germany 2027-28, EU ViDA 2030)

- **Problem:** Multinationals must issue and receive structured e-invoices through country-specific networks and clearance platforms on rolling deadlines. Most ERPs and AP flows aren't ready, and readiness is poor.
- **Who has it:** Tax, AP/AR and IT at every company trading in the EU. Hundreds of thousands, with roughly 50K multinationals.
- **Evidence:** Only 24.6% of 828 medium and large Belgian organizations could both send and receive e-invoices in the months before the mandate (https://e-invoicing-compliance.basware.com/en/the-countdown-to-belgiums-e-invoicing-mandate-where-do-companies-stand). Poland KSeF and the France Sep 2026 rollout (https://blogs.opentext.com/e-invoicing-europe-2026-lessons-from-poland-belgium-greece-france-and-germany/).
- **Existing solutions:** Sovos, Avalara, Pagero (Thomson Reuters), Basware, Comarch, Vertex, plus many Peppol access points.
- **Why it matters long-term:** Once every invoice is structured and real-time, invoice-level audits and contract enforcement (#2, #3, #4) become much easier. This is an enabler.
- **Verdict: WEAK** as a wedge (compliance plumbing, crowded, EU-centric). It is a STRONG tailwind for #2-#4.

## 22. Sales tax / VAT on AI and digital services (nexus, taxability of tokens and agents)

- **Problem:** SaaS and AI companies selling globally face changing taxability rules for digital services, AI and data, plus economic nexus in 45+ states and VAT in 100+ countries.
- **Who has it:** Finance at SaaS/AI companies.
- **Evidence:** Anrok raised a $55M Series C in Oct 2025 at a $525M valuation. It has 3,000+ customers, and 40% of the Forbes AI 50 use it (https://www.sacra.com/c/anrok, https://multiples.vc/private-comps/anrok).
- **Existing solutions:** Anrok, Avalara, Vertex, Numeral (YC; funding to verify), Stripe Tax.
- **Verdict: WEAK.** Anrok, Numeral and Stripe Tax already lead, so the gap is closing.

## 23. Agentic B2B commerce: governing purchases made by AI agents (authority, spend policy, audit trail, liability)

- **Problem:** As procurement and employee agents start buying (and supplier agents start quoting and negotiating), companies have no way to give an agent a scoped mandate (budget, approved vendors, contract terms), verify a counterparty agent, or reconcile and audit what agents committed to.
- **Who has it:** CFOs, CPOs and controllers at early-adopter enterprises now, and essentially all mid-market and enterprise companies by 2028-2030.
- **Evidence:**
  - Gartner (via elogic): "90% of all B2B purchases could be handled by AI agents by 2028, driving over $15 trillion" (https://elogic.co/blog/ai-agents-b2b-buying/).
  - Forrester: about 1 in 5 B2B sellers face agent-led quote negotiations by end of 2026 (same source).
  - Protocols exist: MCP, OpenAI-Stripe ACP (Sep 2025), Google UCP (Jan 2026), Visa Intelligent Commerce and Mastercard Agent Pay.
  - Pactum ($54M Series C, Jun 2025) already runs AI supplier negotiations for Walmart (https://www.shopifreaks.com/?p=8688).
  - Skyfire ($8.5M seed) is building agent payment rails (https://techcrunch.com/2024/08/21/skyfire-lets-ai-agents-spend-your-money).
  - Activant research page on agentic procurement (https://activantcapital.com/research/agentic-procurement).
- **Economic pain:** Mostly prospective today. It looks like policy and fraud control for a new spend channel, so pain will scale with agent spend volume.
- **Existing solutions:** Payment rails (Skyfire, Payman, Natural, Stripe, Visa, Mastercard), card controls (Ramp, Brex), negotiation agents (Pactum, Fairmarkit at $78M total). Nobody owns the "agent mandate + contract + audit" layer for the corporate buyer.
- **Why now:** The protocols landed in 2025-26, and the Gartner and Forrester timelines put adoption in 2026-2028.
- **Risk:** Early. Real B2B agent purchasing volume in 2026 is small, and Ramp, Brex, Stripe and the card networks will push to own the control layer.
- **Verdict: MEDIUM (high upside).** It's the best long-term story, but buyers may not feel acute pain until 2027-28. The best entry is probably through #5 (AI spend control) or #3 (contract enforcement), extended to agent-originated transactions.

## 24. FP&A data wrangling, headcount and vendor-level forecasting

- **Problem:** FP&A teams spend most of their time pulling and cleaning data from the ERP, HRIS, CRM and billing into Excel before any analysis happens.
- **Evidence:** Category is mature, with Pigment, Anaplan, Adaptive, Cube, Runway and Abacum all funded. AI-native ERPs and "AI analyst" startups are crowding in (no strong new evidence retrieved this session).
- **Verdict: WEAK.** Saturated with well-funded players.

---

## Top 5 most promising

1. **Contract-to-cash enforcement layer (buy side) — #2 + #3.** AI that reads every supplier contract and price-increase letter and audits every invoice line against it (escalators, surcharges, rebates, tiers, MFN, SLA credits), then recovers the money.
   - One-liner: "we find and recover the money your suppliers owe you under contracts you already signed."
   - The 2025-26 tariff volatility gives it an urgent hook, and there are hard dollars on a contingency or fee basis.
   - Competition: Rivvun (seed), Enable (rebates only), legacy recovery auditors (PRGX). Real, but early.
   - ACV of $100K+ is plausible for $500M+ spenders.
2. **AI/agent spend control and unit economics — #5 + #6 + #16.** A system of record for AI and consumption spend: attribution to team, agent, product and customer; forecasting; budget enforcement; vendor invoice verification.
   - It rides the clearest 2027-2032 trend (token volume up 60x+ in 15 months, Uber blowing its budget).
   - The risk is bundling by Ramp, Datadog or cloud FinOps vendors, so the differentiator must be agent-level cost accounting and AI COGS, not dashboards.
3. **Sell-side revenue leakage recovery — #4 (+ #15).** AI that reconciles signed contracts against invoices and usage to catch unbilled escalators, minimums, overages and true-ups.
   - Self-funding ROI, and the problem gets worse as AI pricing makes contracts hybrid.
   - Natural pair with #1 as one "contract execution" platform over the ERP.
4. **Tariff refund and surcharge pass-through reconciliation — #1 → #2.** It starts as a time-boxed wedge: reconstruct who paid IEEPA duties and surcharges and settle the B2B claims.
   - That wedge earns access to every importer's and buyer's invoice and contract data, which becomes ongoing surcharge and tariff governance.
   - Very fast pilots and urgent buyers, but the product must evolve or it stays a services business.
5. **Agentic B2B commerce governance — #23.** Mandates, policy, counterparty verification and audit trails for purchases agents make.
   - The most category-defining story ("the control plane for corporate purchases made by AI agents"), but the least proven current pain.
   - Best pursued as the long-term expansion of #1 or #2 rather than as the initial wedge.

**Skeptical take:** #1 and #3 overlap heavily and could be one company: "the enforcement layer between contracts and money." Most of the other problems (cash app, duplicates, renewals, intake, sales tax, FP&A) are crowded and owned by funded leaders, so they are weak wedges for a new $1B company.
