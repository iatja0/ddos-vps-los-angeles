# DDoS Protected VPS Los Angeles: How Many Gbps Do You Actually Get, Is Filtering Always-On, and Which LA Datacenter Are You In? (SixtyNet's LAX Plans vs. the Budget Market)

Three things decide whether a Los Angeles DDoS-protected VPS survives an attack: the mitigation ceiling in Gbps, whether filtering is always-on or only engages after detection, and whether protection reaches layer 7 at all. A $4.50 plan and a $130 plan can both print "DDoS protected" on the order page and behave nothing alike when 20Gbps of UDP garbage shows up.

SixtyNet's Los Angeles catalog splits into two product families, and only one of them belongs in this conversation. The LAX plans carry a DDoS Protection label and start at **$200/year** for 2 cores, 2GB RAM, 40GB NVMe and 5TB of traffic on a 2G port, down from a $240 list price. What the site does not publish is the mitigation capacity in Gbps, whether filtering runs continuously, or which building in Los Angeles the hardware sits in. Those three omissions are what this article is organized around, because they are exactly what determines whether the thing holds up on the night someone decides to ruin your week.

## The three-question check, before you compare a single price

> **Ask any host these in a presales ticket:**
> 1. What is the mitigation capacity in Gbps, and what happens to my IP above that ceiling?
> 2. Is traffic always filtered through the mitigation path, or rerouted only after an attack is detected?
> 3. Does the protection cover layer 7, or stop at L3/L4?

If a sales page answers none of them, that is not proof of a bad product. It is proof that you cannot tell yet, and the ticket reply is the only thing that will settle it. Keep the reply.

👉 [Check SixtyNet's current LAX DDoS-protected plan pricing](https://sixtynet.net/aff.php?aff=39)

## SixtyNet's three LAX plans, side by side

| Plan | CPU / RAM | Storage | Traffic / Port | Annual price | Order |
| --- | --- | --- | --- | --- | --- |
| LAX-STARTER | 2 cores / 2GB | 40GB NVMe | 5TB / 2G | $200/yr (list $240) | [Start with LAX-STARTER](https://sixtynet.net/aff.php?aff=39) |
| LAX-MEDIUM | 8 cores / 8GB | 160GB NVMe | 20TB / 10G | $800/yr (list $960) | [See LAX-MEDIUM annual pricing](https://sixtynet.net/aff.php?aff=39) |
| LAX-LARGE | 8 cores / 16GB | 320GB NVMe | 40TB / 10G | $1,600/yr (list $1,920) | [See LAX-LARGE annual pricing](https://sixtynet.net/aff.php?aff=39) |

Two things stand out in that table.

The scale-up is linear. Going from STARTER to MEDIUM quadruples cores, RAM, storage and traffic and takes the port from 2G to 10G, for four times the money. There is no pricing cliff to game and no obvious "sweet spot" plan. You pick the size you need and pay proportionally, which is at least honest.

The LARGE tier keeps 8 cores. Compared with MEDIUM, the extra $800 a year buys RAM (8GB to 16GB), storage (160GB to 320GB) and traffic (20TB to 40TB). If your workload is CPU-bound, LARGE is a bad deal; if you're stacking containers or a database that wants memory, it's the only option in the lineup.

All three show "DDOS Protection" in the feature list. None of them shows a number next to it.

## Before you go further: the two other product lines, and why they're not for this

SixtyNet's VPS hosting page also lists residential-IP plans, and readers hunting "DDoS protected VPS Los Angeles" keep landing on them by mistake.

- **Residential-STARTER**: 2 cores, 2GB RAM, 40GB NVMe, 5TB traffic, **$260/year** (list $300).
- **Residential-LARGE**: 16 cores, 16GB RAM, 320GB NVMe, 40TB traffic, **$1,660/year** (list $1,980).

These carry a residential IP and no DDoS Protection tag, and the page states plainly that residential IP products **do not open ports 80 and 443** for IP risk-control reasons. If you're planning to host a website, that disqualifies the whole family regardless of price. The LAX plans are the ones built for public-facing workloads.

The page also displays one further configuration — 4 cores, 4GB RAM, a 300GB volume plus 200GB bonus in RAID10, 10TB traffic and a DDoS Protection label — without a visible price. Worth asking about if that shape fits you better than the LAX tiers.

One more ambiguity: the top of the VPS page advertises China Unicom AS9929 routing, free BGP session setup and 95th-percentile billing. Whether those apply to the LAX VPS plans specifically is not spelled out; the plans themselves only say "2G Premium Network" or "10G Premium Network." If China-optimized routing is the reason you're shopping, get that confirmed rather than assumed.

## What "DDOS Protection" on a spec sheet is worth

Three questions again, this time with what each answer changes.

**Capacity in Gbps.** This is the ceiling, not a quality rating. A host offering 10Gbps of mitigation and a 40Gbps flood ends the same way as no protection: your box goes dark. 60Gbps headroom covers essentially every grudge flood, botnet UDP spray and SYN flood a small game server or IRC network will ever see. A single-digit ceiling covers most of them too, until it doesn't.

**Always-on vs. on-demand.** Always-on means clean traffic and attack traffic both travel the filtering path, so nothing changes when an attack starts. On-demand means the provider notices the attack, then reroutes you, and the detection window is your downtime. Seconds to minutes, every time. For a game server that's a player wipe; for a brochure site it's a shrug.

**Layer 3/4 vs. layer 7.** Network-layer scrubbing filters packets. A slow HTTP request flood that ties up your web workers looks like legitimate traffic at that layer and passes straight through. If that's your threat model, you need a WAF in front, and no budget VPS's included protection replaces it.

Here's where LA hosting gets interesting. Of the four providers worth comparing in this market, only two publish a Gbps figure at all. RackNerd's Los Angeles DC-05 line advertises **60Gbps** of mitigation; Global Frag Networks puts **10Gbps** of mitigation on every VPS plan. ExtraVM's Los Angeles page describes "high-capacity" protection from Global Secure Layer plus local eBPF/XDP filtering, and claims coverage of both volumetric and application-layer attacks, without a number. SixtyNet's LAX page says "DDOS Protection" and stops there.

That ExtraVM claim is worth reading carefully. A vendor's own page asserting application-layer coverage is a vendor claim, not an industry standard, and most low-cost LA hosts only ever mean L3/L4. Treat it as a question to verify in a ticket, not a category truth.

👉 [See what the LAX-STARTER plan currently includes](https://sixtynet.net/aff.php?aff=39)

## A 10G port is not 10Gbps of protection

This confusion costs people money. SixtyNet's LAX-MEDIUM and LAX-LARGE list a "10G Premium Network." That's port speed: how fast traffic can flow in and out of your VM. It says nothing about how much attack traffic the scrubber in front of you can absorb before it gives up and blackholes the IP.

The two numbers are independent. You can have a 10G port behind 2Gbps of mitigation and lose to a 3Gbps flood. You can also have a 1G port behind 60Gbps of mitigation and stay online through an attack ten times your pipe. When you read a spec sheet, find the port speed and the mitigation capacity separately. If only one number appears, it's the port.

## Which "Los Angeles" you're actually in

Four providers, four different buildings, and the differences are real.

ExtraVM hosts in **Digital Realty BUR10** at 3015 Winona Ave in Burbank, a Tier-IV carrier-neutral facility, and publishes latency figures from it: 5–30ms across the western US, 60–80ms to the east coast, 110–150ms to Tokyo, 160–180ms to Singapore. RackNerd's DC-05 sits in the **One Wilshire** building downtown, on an Asia-optimized BGP blend with a public test IP. Global Frag Networks operates out of **900 N. Alameda Street**. SixtyNet's LAX page says Los Angeles and nothing more specific.

Los Angeles is the main US landing point for trans-Pacific submarine cables, so a genuinely well-connected LA node is the lowest-latency US option for users in Japan, Korea, Taiwan, Hong Kong and Southeast Asia. But "Los Angeles" as a label spans roughly 20 miles, and the building plus the return route can move your Tokyo latency by tens of milliseconds. If latency is why you chose LA, ask for the street address and a test IP before you order.

## What the price difference buys

| Provider | LA location | Protection as stated | Entry price |
| --- | --- | --- | --- |
| ExtraVM | Digital Realty BUR10, Burbank | Global Secure Layer + local eBPF/XDP; vendor claims volumetric and application layer | $4.50/mo (1GB) |
| RackNerd | One Wilshire, downtown LA (DC-05) | 60Gbps, always-on | 1.5GB tier around $30/yr per third-party writeups; confirm on site |
| Global Frag Networks | 900 N. Alameda St | 10Gbps mitigation per VPS | Not published on site |
| SixtyNet | Los Angeles, building not stated | "DDOS Protection," Gbps not published | $200/yr (LAX-STARTER) |

SixtyNet's $200 a year works out to roughly $16.70 a month. ExtraVM's closest comparable shape, 2GB RAM with 5TB of traffic, is $8 a month or $96 a year. So SixtyNet runs about twice the price for twice the cores (2 vs 1), more storage (40GB vs 30GB) and a wider port.

Whether that's worth it depends on what you're buying the machine for. Per gigabyte of RAM, SixtyNet's LAX-STARTER is not a bargain against the cheapest end of this market. What you're paying for is a bigger box with a 10G-capable network path available one tier up, and a provider that has chosen to compete on hardware rather than on a $30 annual doorbuster. If your budget ceiling is $50 a year, SixtyNet isn't in your range and no amount of framing changes that.

## Who should skip DDoS-protected hosting entirely

If nothing you run has ever attracted an attacker and nothing is likely to, the protection premium is money you don't need to spend. A plain VPS does the same job.

If you're taking sustained multi-hundred-Gbps floods, state-adjacent traffic, or layer-7 request floods, none of these budget plans will save you. You're in Cloudflare paid tiers or a dedicated scrubbing provider territory, layered in front of whatever box you rent. That's a threat model that outgrew budget hosting, not a provider failure.

And if you need ports 80 and 443 for a website, stay away from residential-IP plans at any provider. They're built for a different job.

## FAQ

**Does a 10Gbps port mean 10Gbps of DDoS protection?**
No. Port speed is throughput capacity. Mitigation capacity is a separate number and is usually smaller.

**Does always-on filtering add latency to normal traffic?**
Filtering typically happens at the network edge on dedicated hardware, and clean traffic passes through the mitigation path rather than being detoured. The added latency is usually small, but it varies by provider and by route. Ask the specific host for a before-and-after figure rather than trusting a general answer.

**What's the refund situation?**
SixtyNet's checkout terms are the authoritative source, and one detail is already visible: on the secured residential-IP variant, the page states that refunds are issued only as site balance. A third-party review of SixtyNet mentions a 3-day money-back window, which would be far shorter than the 7 to 30 days common in this market. Confirm the exact window for the plan you're buying before paying, and screenshot it.

**Can I host a public website on it?**
On the LAX plans, nothing on the page restricts ports 80 and 443. On the residential plans, those ports are explicitly closed.

**Can I upgrade later?**
Not documented on the plan pages. Ask in the ticket alongside the Gbps question.

## How to decide

- A small game server, a VPN endpoint, a proxy, or a low-traffic site that has been attacked before → **LAX-STARTER at $200/year**. 2 cores and 2GB handles those workloads fine, and 5TB of traffic is far more than they'll use.
- Multiple services, a real database, Docker containers, or more than a handful of concurrent users → **LAX-MEDIUM at $800/year**. The 8 cores and 10G port are the actual reason to move up.
- Memory-hungry workloads that are not CPU-hungry → **LAX-LARGE at $1,600/year**, knowing you're paying double for RAM, storage and traffic while the core count stays at 8.

Two things to nail down before you pay. First, get the mitigation capacity in Gbps and the always-on answer in writing, in a ticket reply you keep. Second, confirm the refund window and the renewal price, then screenshot both. Neither is a reason to avoid the provider; both are reasons not to guess.

👉 [Compare SixtyNet's LAX plans and current annual pricing](https://sixtynet.net/aff.php?aff=39)
