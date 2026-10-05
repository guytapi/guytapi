# Round 11: Forced Migrations, 2026-2029

*Analyst: skeptical research pass, 2026-10-05. 39 web searches. WebFetch was not used, so every figure below comes from search-result snippets. Most are secondary sources (consultancies, vendor blogs, trade press). Anything marked **[unverified]** is my own estimate or a single-source claim.*

## TL;DR verdict

**The lens fails the bar.** Forced migrations are real, large and urgent. But three structural forces kill most of them as venture theses:

1. **The destination vendor pays for the migration.** Whoever wins the workload ships a free AI migration agent: AWS Transform (VMware), Red Hat MTV + Lightspeed/MCP agents (mid-2026), Nutanix Move, Platform9 vJailbreak (open source), Snowflake SnowConvert AI + AIM Migration Agent (Informatica/SSIS), Databricks Lakebridge, Microsoft Sentinel SIEM-migration (SPL to KQL), Elastic Express Migration, Oracle's EBS/JDE-to-Fusion configuration agent, and Adaptavist's ScriptRunner Migration Agent for Atlassian. This is platform absorption with a twist: the platform is the *destination*, not the source.
2. **Horizontal "migration agent" companies are already funded and big.** Tessera Labs ($60M Series A, a16z, $320M post-money; covers SAP, Salesforce, Workday and Oracle), Nova Intelligence ($31.5M, SAP), Blitzy ($200M, codebases), Mechanical Orchard ($50M B, GV), Hypercubic (YC, $5.3M seed, mainframe), Datafold Migration Agent and Matillion Maia Migration Agent (ETL).
3. **Migration is a one-time event (the services trap).** The "then become the ops layer" story mostly collides with the new system's own console (Prism, OpenShift, RCA, Atlassian Cloud).

The best two candidates, (1) a vendor-neutral VMware estate exit and (2) a Salesforce CPQ exit/rebuild, score **6.2** and **5.7**. Neither clears 8.5. Both are written up below for completeness.

---

## 1. Survey of forced migrations

| Migration | Hard date / shock | # affected | $ per migration | AI-native / tool players | Services trap? | Verdict |
|---|---|---|---|---|---|---|
| **Broadcom/VMware** | Perpetual licences gone; 8,000 SKUs collapsed into 2 bundles; 72-core minimum (Apr 2025); increases of 150-1,500% (AT&T: 1,050%); renewals running through 2026 | 300K+ customers. Broadcom focuses on its top 10K, and 87% of those took VCF, but the average customer renews only ~25% of its estate. 48% plan to reduce footprint by 2028; 87% are actively reducing but only 4% have fully migrated. Nutanix claims ~30K migrated customers. Gartner: 70% of enterprises move ≥50% of workloads by 2028 | Gartner: $300-3,000 per VM; 18-48 months for estates of 2,000+ VMs; $1.6-3.4M per 10K VMs to Nutanix | Free: Nutanix Move, Red Hat MTV (+ AI agents mid-2026), Platform9 vJailbreak, AWS Transform, Azure Migrate. SIs: Tech Mahindra "AI-led VMware exit", LTIMindtree, Rackspace. Multi-hypervisor management: HPE Morpheus, Proxmox Datacenter Manager. **No funded AI-native neutral startup found** | Partly. Moving the VM disks is commoditized; the surrounding estate (NSX, automation, DR, runbooks) is not | **Top pick #1 (6.2)** |
| **Atlassian Data Center EOL** | End of sale to new customers 30 Mar 2026; existing customers' last renewal 30 Mar 2028; **read-only 28 Mar 2029**; DC price +15% from Feb 2026 | "99% in cloud or on a path"; DC customers often have tens of thousands of users. Exact DC customer count **[unverified]** | Example: 2,000-user enterprise pays ~$405K in Year 1 (licence + PS + partner + apps + parallel running) | Atlassian JCMA/CCMA (free) plus funded partner programs; Adaptavist ScriptRunner Migration Agent (AI script conversion); Cprime "AI + expertise"; exit destinations (GitLab, Azure DevOps, ONES) each run their own migrations | Yes. The source vendor *wants* the move and funds partners | Kill: absorbed by the source vendor and its ecosystem |
| **Salesforce CPQ** | End of sale Mar 2025; EOL "~2029-2030" expected but **not formally dated [unverified]** | CPQ installed base **[unverified: est. 5-12K orgs]**. Only ~15% of RCA customers are CPQ migrants, so most have not moved yet | $100-500K reimplementation; "no automated migration tool"; RCA is a full rebuild (custom managed-package objects to standard objects) | SIs (Accenture-tier down to Grazitti/Simplus); Prodly migration tool; displacement offers from DealHub, Nue and Conga; Tessera (Salesforce in scope) | Mostly | **Top pick #2 (5.7)** |
| **SAP ECC 2027** | Mainstream support ends 2027 | Large | $M+ | Nova ($31.5M), Tessera ($60M, a16z), SAP itself | n/a | Kill: crowded |
| **Dynamics GP** | Enhancements and support end 31 Dec 2029; security updates end 30 Apr 2031 | Tens of thousands of SMB/mid-market orgs **[unverified]** | $50-250K **[unverified]** | Microsoft partners, BC migration tools | Yes | Kill: SMB ACV, partner channel owns it |
| **Oracle EBS / JDE** | **Not forced**: EBS 12.2 Premier Support extended to ≥2037, JDE 9.2 to ≥2036 | Large | Large | Oracle Fusion config agent, Oracle Soar | n/a | Kill: no forcing function |
| **Informatica PowerCenter** | Standard support ended **31 Mar 2026**; extended to Mar 2027; sustaining to 2029. Salesforce closed the $8B acquisition Nov 2025 | Thousands **[unverified]** | $0.5-5M **[unverified]** | Informatica's own path to IDMC, SnowConvert/AIM, Lakebridge (BladeBridge), Datafold Migration Agent, Matillion Maia, Bitwise, LeapLogic | Destination-absorbed | Kill: urgent now, but the most crowded of all |
| **Splunk under Cisco** | 9%/yr renewal uplift; ES at 500 GB/day costs $1.2-2.5M/yr; 62% "evaluating alternatives" | Thousands of enterprises | $400-800K in Year 1 (rule translation, 6-12 months of parallel running) | Cribl (Detect, assisted translation), SOC Prime Uncoder, Sentinel migration, CrowdStrike, Elastic Express, Google SecOps, MDRs | Destination-absorbed | Kill: every SIEM vendor funds the switch |
| **Datadog bill shock** | Custom-metric and cardinality billing | Many | Low-to-mid | OTel Collector dual-export; Dash0, groundcover, Coralogix, OneUptime guides | Yes | Kill: crowded; OTel commoditizes the switch |
| **Heroku** | "Sustaining engineering" from 6 Feb 2026; no new Enterprise contracts | Many SMB/dev teams | Low | Render, Qovery, Aptible, DigitalOcean, Encore | Yes | Kill: SMB ACV |
| **Citrix (CSG)** | Universal bundles; renewals up 50-300%; file-based licensing EOL 15 Apr 2026; 250-user minimum | Thousands | Mid | Nerdio, Omnissa (also raising prices +7-21%), Inuvika, Accops, Azure Virtual Desktop/W365 | Yes | Kill: Microsoft/Nerdio absorb it |
| **Terraform to OpenTofu, Redis, Elastic** | Licence changes, partly reversed (Elastic AGPL, Redis AGPL) | Many | Low (often drop-in) | Spacelift, env0, Scalr, Valkey | n/a | Kill: drop-in, so little pain |
| **Legacy BI (Cognos, MicroStrategy, Tableau)** | No hard EOL; MicroStrategy's bitcoin pivot adds strategy risk | Thousands | Mid | Microsoft/Avanade, MAQ MigrateFAST, NousMigrator | Yes | Kill: Microsoft-subsidized, no forcing date |
| **Hadoop/Cloudera, Teradata** | HDP/CDH support ended 2021-22 | Shrinking tail | High | Snowflake/Databricks free tools, Datafold | Yes | Kill: late tail, absorbed |
| **Mainframe (non-bank)** | No forced date | Hundreds-low thousands of non-FS orgs | $M+ | Mechanical Orchard ($50M), Hypercubic (YC), AWS Transform mainframe, IBM watsonx Code Assistant for Z | n/a | Kill: buyers are mostly banks/gov (excluded) and the space is funded |

**Pattern:** the only migrations without a well-funded "free mover" are those where the **destination is fragmented, open source or small** (Proxmox, multi-hypervisor) or where the **source vendor's successor product is weak and the migration is a rebuild** (CPQ to RCA).

---

## 2. Top pick #1: VMware Estate Exit, "everything but the disks"

**One-sentence pitch:** An AI agent that reads your entire vSphere estate (NSX firewall policies, PowerCLI/vRO/Aria automation, backup and DR jobs, monitoring and runbooks), rebuilds it for Proxmox, Nutanix, OpenShift or Hyper-V, proves equivalence before cutover, and then stays on as the hypervisor-neutral operations layer.

**Buyer:** Head of infrastructure or VP IT Ops at companies with 300-5,000 VMs that are hit by the 72-core minimum and the VCF bundle. That is mostly mid-to-upper mid-market and the "non-top-10K" segment Broadcom deprioritized. Excludes banks, government and insurers.

**Buyers x ACV math [estimates]:**
- Addressable: 300K VMware customers. Perhaps 25-40K have more than 200 VMs and are non-regulated **[unverified]**.
- Migration fee: ~$100/VM × 1,500 VMs = $150K one-time. Ops layer: $60-120K/yr.
- **$10M ARR:** ~70 customers on the ops layer at $90K plus migration revenue, about 0.2% of the addressable base.
- **$100M ARR:** ~800-1,000 customers at ~$100K blended, about 3% of the base. Feasible on paper, but it requires the ops layer to retain customers after the migration ends.

**Why now:** 2026 is the "most critical renewal year." Customers renew only ~25% of their estates, which means partial exits and dual-hypervisor estates are the norm. Gartner's figures (18-48 months, $300-3,000/VM) describe exactly the labor LLM agents compress: translating NSX rules into nftables/OVN/Flow policies and PowerCLI into Ansible/Terraform. Only 4% have fully migrated, so the backlog is huge.

**Why incumbents and SIs can't:**
- Each destination vendor's tool moves VMs *to itself* and ignores the surrounding estate.
- Broadcom will not help anyone leave.
- SIs bill by the hour and cannot price an outcome per VM.
- Proxmox (a small Austrian company that is popular but has thin enterprise tooling) leaves an enterprise-operations gap.

**30-90 day pilot:** Pick one cluster or app wave of 100-300 VMs. The agent produces the dependency map plus a converted NSX policy set, automation and backup jobs, and a parity report. The customer executes the cutover with the free mover (Move/MTV/vJailbreak). Success metric: engineering hours per VM against the customer's previous wave.

**Expansion to a recurring platform:** A multi-hypervisor control plane (policy, automation, DR, cost) across the VMware remnant plus 1-2 new hypervisors. The "25% renewal" fact means most customers stay dual-stack for years.

**Moat:** A corpus of estate-translation mappings (NSX constructs, vRO workflows, ecosystem integrations) and validation harnesses. It is weak. The second-best moat is being the neutral ops layer in a dual-stack world.

**Kill risks:**
1. Red Hat's AI-enhanced MTV (Lightspeed + MCP agents, mid-2026) and AWS Transform expand into network and automation translation.
2. "The estates that could leave have left." The peak may be 2024-26, before this company could reach scale.
3. HPE Morpheus and Nutanix already sell multi-hypervisor management.
4. It slides into a services business if parity checking can't be automated.
5. Market timing: VMware revenue is still growing (+13% YoY in Q1 2026), so lock-in is holding for the top 10K.

**Scores (1-10):**

| Pain | Urgency | ROI clarity | Accessibility | Pilot speed | Market size | Expansion | Venture potential | Defensibility | Why now | Competition position | **Avg** |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 8 | 7 | 8 | 6 | 6 | 7 | 5 | 6 | 4 | 7 | 4 | **6.2** |

---

## 3. Top pick #2: CPQ Exit, "rebuild Salesforce CPQ in 30 days, then own pricing-logic change management"

**One-sentence pitch:** An agent that reverse-engineers a Salesforce CPQ org (price rules, product rules, bundles, QCP JavaScript, approvals, templates), regenerates it in Revenue Cloud Advanced (or DealHub/Nue/Conga), proves quote-for-quote parity against historical quotes, and then becomes the test-and-deploy layer for every future pricing change.

**Buyer:** VP RevOps or the Salesforce platform owner at B2B companies with complex catalogs: SaaS, industrial manufacturing, medtech devices (non-regulated buyer side), high tech.

**Buyers x ACV math [estimates]:**
- Addressable: CPQ orgs ~5-12K **[unverified]**.
- Migration: $100-150K, against SI quotes of $100-500K (cited range). Recurring "pricing CI/CD + parity testing": $40-60K/yr.
- **$10M ARR:** ~200 recurring customers at $50K, or migrations plus recurring at ~80 logos. Feasible.
- **$100M ARR:** would need ~2,000 recurring customers, about 20-40% of the base. **Not credible** without expanding into general quote-to-cash and pricing operations beyond CPQ refugees. This caps market size.

**Why now:** End of sale March 2025; "no automated migration tool"; RCA is a ground-up rebuild on different objects; only ~15% of RCA customers are migrants, so the backlog is mostly untouched. Agentforce Revenue Management messaging pushes customers toward 2026-27 budgets ("a 2026 budget line"). Parity testing against thousands of historical quotes is an ideal LLM-plus-deterministic-verifier task.

**Why incumbents and SIs can't:** SIs earn more from manual rebuilds. Salesforce wants RCA adoption but has historically left migrations to partners. Competing CPQs only migrate toward themselves. A destination-neutral tool can also act as a negotiation lever against Salesforce.

**30-90 day pilot:** Ingest one CPQ org. Within 30 days, generate the RCA configuration in a sandbox plus a parity report on the last 12 months of quotes (target: ≥95% exact price match, with an explained diff list). Within 60-90 days, cut over one product line.

**Expansion:** Pricing-change CI/CD (regression-test every price-book or rule change against the quote corpus), catalog governance, and agent-safe pricing APIs for Agentforce quoting agents.

**Moat:** The parity-test corpus per customer creates switching costs. Mapping CPQ patterns to RCA is learnable by anyone, so the moat is weak.

**Kill risks:**
1. **Salesforce ships a native CPQ-to-RCA migration agent.** This is highly plausible: Agentforce-everything plus a strategic interest in RCA adoption.
2. Tessera Labs ($60M, a16z) already lists Salesforce in scope.
3. Gearset, Copado and Prodly (Salesforce DevOps vendors) add pricing CI/CD.
4. No hard EOL date, so customers procrastinate.
5. TAM ceiling is roughly $50-80M ARR.

**Scores (1-10):**

| Pain | Urgency | ROI clarity | Accessibility | Pilot speed | Market size | Expansion | Venture potential | Defensibility | Why now | Competition position | **Avg** |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 7 | 5 | 7 | 7 | 7 | 5 | 5 | 5 | 4 | 6 | 5 | **5.7** |

---

## 4. Lessons for STATUS.md

- **New killer: destination subsidy.** In a forced migration, the vendor winning the workload gives migration away free and increasingly AI-driven, so a migration startup needs a destination with no deep-pocketed owner.
- **Horizontal "AI migration factory" is taken** (Tessera, Blitzy, Nova, Mechanical Orchard, Datafold). Vertical migration wedges are features of these companies or of destination vendors.
- **The surviving shape:** fragmented or open-source destinations (Proxmox/KVM) or rebuild-style successor products (CPQ to RCA). Both are services-heavy, and the "post-migration ops layer" competes with the new system's own console.
- If the founders pursue this lens, the only test worth running is 10 calls with infrastructure heads in the 300-5,000-VM segment. Ask: did your VMware exit cost go to VM moving or to the surrounding estate, and would you pay per VM for the estate part?

---

## Sources (from search results; not fetched or verified beyond snippets)
- VMware survey (48% reduce by 2028): https://www.storagenewsletter.com/2026/04/06/48-of-vmware-customers-plan-to-reduce-usage-as-competitors-gain-ground/
- Nutanix ~30K migrations: https://feedbagel.com/post/nutanix-reports-30000-vmware-customer-migrations-following-broadcom-acquisition
- Gartner exodus by 2029: https://www.sdxcentral.com/news/vmware-rivals-circle-as-gartner-predicts-55-enterprise-exodus-by-2029/
- Gartner cost per VM: https://www.lemondeinformatique.fr/actualites/lire-gartner-prevoit-des-migrations-hors-vmware-longues-et-couteuses-95819.html ; https://www.cloudmagazin.com/en/2026/03/18/vmware-broadcom-kostenfalle-2026-alternativen-proxmox-nutanix/
- Broadcom pricing (72-core, 150-1,500%): https://redresscompliance.com/broadcom-vmware-price-increases-enterprise-benchmarks.html ; https://www.it-daily.net/en/shortnews-en/vmware-licensing-broadcom-raises-core-minimum-to-72-cores
- Broadcom top 10K / 25% renewal: https://www.networkworld.com/article/4180754/will-broadcoms-vmware-strategy-keep-paying-big-dividends.html
- AWS Transform VMware: https://aws.amazon.com/about-aws/whats-new/2025/12/transform-vmware-agentic-ai-enterprise-migration/
- Platform9 vJailbreak: https://www.sdxcentral.com/news/platform9-offers-jailbreak-for-vmware-migration/
- Red Hat OpenShift Virtualization / MTV AI: https://redhat.com/en/blog/virtualization-2026-building-platform-vms-containers-and-ai ; https://adtmag.com/articles/2026/05/15/red-hat-expands-openshift-virtualization.aspx
- Tech Mahindra AI-led VMware exit: https://www.techmahindra.com/services/cloud-infrastructure-services/data-center-services/scaled-ai-led-vmware-exit-and-modernization/
- Atlassian DC EOL dates: https://us.seibert.group/blog/end-of-life-atlassian-data-center ; https://www.schneider.im/atlassian-data-center-end-of-life/
- Atlassian migration cost example: https://redresscompliance.com/atlassian-cloud-migration-guide-2026.html
- ScriptRunner Migration Agent: https://www.scriptrunnerhq.com/atlassian-apps/jira/scriptrunner-migration-suite
- Atlassian FY26 DC commentary: https://www.sec.gov/Archives/edgar/data/0001650372/000165037226000031/teamq42026shareholderlet.htm
- Salesforce CPQ EOS: https://www.salesforce.com/sales/cpq/end-of-life/
- CPQ reimplementation $100-500K, no automated tool: https://redresscompliance.com/salesforce-revenue-cloud-cpq-licensing.html
- Prodly CPQ-to-RCA: https://www.prodly.co/videos/cpq-to-revenue-cloud-migration
- DealHub displacement: https://dealhub.io/salesforce-cpq-sunsets/ ; Nue: https://www.nue.io/resources/articles/salesforce-cpq-nue-migration/
- Informatica PowerCenter support dates: https://www.tarento.com/articles/informatica-powercenter-end-of-support-migration/
- Datafold Migration Agent: https://www.datafold.com/blog/datafold-migration-agent-now-supports-all-major-etl-tools/
- SnowConvert ETL: https://docs.snowflake.com/en/migrations/converting-etl
- Matillion Maia Migration Agent: https://www.morningstar.com/news/pr-newswire/20260326ln20484/matillion-launches-maias-migration-agent-autonomous-migration-for-legacy-etl-platforms
- Splunk migration cost / Cribl: https://www.techtarget.com/it-infrastructure/news/366651477/Cribl-targets-SIEM-data-costs-with-new-Detect-tool ; https://underdefense.com/blog/best-managed-siem-for-companies-moving-off-splunk/
- Splunk renewal economics: https://redresscompliance.com/splunk-renewal-guide.html
- Sentinel SIEM migration: https://learn.microsoft.com/en-US/Azure/sentinel/siem-migration
- SOC Prime Uncoder: https://socprime.com/blog/ai-siem-migration-simplify-optimize-innovate/
- Heroku sustaining engineering: https://render.com/articles/leaving-heroku-migration-guide-2026
- Dynamics GP dates: https://www.forvismazars.us/forsights/2024/10/microsoft-dynamics-gp-end-of-support-announcement
- Citrix pricing: https://getnerdio.com/blog/citrix-price-increase/ ; https://www.inuvika.com/citrix-alternatives-2026-comparison/
- Oracle EBS/JDE extensions: https://erpresearch.com/en-gb/oracle-ebusiness-suite ; Oracle agent: https://www.forrester.com/blogs/oracle-applications-analyst-summit-fusion-agents-are-shifting-from-assist-to-decide/
- Tessera Labs $60M: https://erp.today/erp-modernization-ai-tessera-labs-funding/ ; https://a16z.com/announcement/investing-in-tessera-labs/
- Nova Intelligence: https://www.shopifreaks.com/nova-intelligence-raises-31-5m-series-a-led-by-chemistry-to-bring-agentic-ai-to-saps-89b-migration-wave/
- Blitzy $200M: from the Sky9 Capital summary https://www.sky9capital.com/blog/ai-agent-startups-2026/ **[unverified]**
- Mechanical Orchard / Hypercubic: https://pulse2.com/mechanical-orchard-50-million-series-b-raised-to-help-companies-transition-away-from-legacy-software/amp/ ; https://pulse2.com/hypercubic-raises-5-3-million-seed-to-turn-mainframe-modernization-into-a-software-driven-process/
- Datadog/OTel migration: https://www.dash0.com/guides/migrating-from-datadog-to-opentelemetry-and-dash0
