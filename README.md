# OSINT Toolkit — A Curated Catalog

Most OSINT tool lists are exhaustive dumps: hundreds of overlapping, half-maintained tools you will never open. This one is the opposite — **opinionated and comprehensive at the same time.** It spans every major OSINT need, and for each one it names the tool (or two) actually worth using, says why, and tells you what to skip.

Signal over tool-porn. Every tool links to its **original upstream project** — install from the official source.

> Each category ends with a **Pick:** line: the bottom-line recommendation for that need. If you read nothing else, read those.

---

## 1. Content — extraction and archiving of publications

Tools for downloading, converting and archiving content from publishing platforms.

| Tool | Description | Language | Notes |
|------|-------------|----------|-------|
| **[sbstck-dl](https://github.com/alexferrari88/sbstck-dl)** | A Substack CLI downloader that can grab individual posts or the full archive of any publication. Its strength is session-cookie support: if you are subscribed to a paid publication, you can also download that protected content. Outputs clean Markdown/HTML and respects the original structure. Useful for local copies of newsletters before they disappear. | Go | Single dependency-free binary. |
| **[Substack2Markdown](https://github.com/BootlegRealityShow/Substack2Markdown)** | Converts Substack publications to Markdown and HTML with a navigable index. Unlike sbstck-dl (raw download), it produces a readable, well-structured archive: table of contents, per-post metadata, clean formatting. Good for ingesting newsletters into NotebookLM or RAG systems. | Python | Complementary to sbstck-dl: one downloads, the other formats. |

**Pick:** sbstck-dl to pull the content, Substack2Markdown to make it readable. That pair covers Substack archiving end to end.

---

## 2. Environments — preconfigured working systems

Distributions or virtual machines with OSINT tools already installed, ready to work.

| Tool | Description | Base | Notes |
|------|-------------|------|-------|
| **[tlosint-live](https://github.com/tracelabs/tlosint-live)** | An OSINT virtual machine by Trace Labs, based on Kali Linux. Ships with dozens of preinstalled, preconfigured OSINT tools (Maltego, Spiderfoot, theHarvester, recon-ng…), plus browsers with separate research profiles. A complete disposable working environment so you skip hours of setup. ISO or importable VM. | Kali Linux | Great for OSINT CTFs, training, and disposable investigation boxes. |
| **[CSI Linux](https://csilinux.com/)** | An Ubuntu-based forensic and OSINT distribution organized by workflow (online investigations, dark web, SIGINT, forensics). More forensics-oriented than tlosint-live. | Ubuntu | Reach for it when the work is forensic. |

**Pick:** tlosint-live for a ready-made, disposable OSINT box; CSI Linux when the work is forensic. *(Buscador, Michael Bazzell's old people-focused distro, is discontinued — kept here only as a historical reference.)*

---

## 3. Frameworks — automated reconnaissance

Reconnaissance engines that integrate multiple modules and data sources. They launch broad searches from a seed value (domain, email, name) and correlate results automatically.

| Tool | Description | Interface | Status |
|------|-------------|-----------|--------|
| **[spiderfoot](https://github.com/smicallef/spiderfoot)** | The reference automated reconnaissance engine. Integrates 200+ modules querying public sources, third-party APIs and threat-intel services. From a seed (domain, IP, email, name, phone, Bitcoin address, ASN…) it launches all relevant modules and correlates results into a graph. Web UI + CLI, report export, alerting. | Web UI + CLI | The most powerful and complete of the group. |
| **[osint_toolkit](https://github.com/deepskydetective/OSINT-Toolkit)** | A full-stack app (FastAPI + React) acting as an analyst dashboard for IOC investigation: given an IP, domain, hash or email it queries multiple APIs (VirusTotal, AbuseIPDB, Shodan…) and consolidates results. A quick-lookup panel, not autonomous recon. | Web UI | Complement to spiderfoot for one-off IOC analysis. |
| **[recon-ng](https://github.com/lanmaster53/recon-ng)** | A modular framework with a Metasploit-style interactive console. Persistent workspaces, integrated database, centralized API-key management. Strong at domains, subdomains, corporate contacts and leaks. The console enables iterative exploration spiderfoot lacks. | CLI (console) | The reference for modular, iterative recon. |

**Reference resource (not executable):** **[OSINT Framework](https://osintframework.com/)** — an interactive link tree of OSINT resources by topic; for finding a tool, not software to run.

**Pick:** spiderfoot is the engine for broad automatic sweeps; recon-ng for hands-on iterative pivoting. Ignore the older all-in-one aggregator clones.

---

## 4. Identity and accounts — people, emails, usernames

| Tool | Description | Scope | Notes |
|------|-------------|-------|-------|
| **[maigret](https://github.com/soxoj/maigret)** | The improved heir to Sherlock and the current standard for username enumeration. Searches a username across thousands of sites, extracting profile metadata. Discards false positives. Reports in HTML/JSON/CSV/PDF. Also supports email search. | Usernames, emails | The most complete in its niche. |
| **[social-analyzer](https://github.com/qeeqbox/social-analyzer)** | Searches profiles by name/username across 1,000+ sites with a match-confidence rating per result, reducing false-positive noise. REST API and cross-account analysis. | Usernames | Complementary to maigret for its scoring. |
| **[holehe](https://github.com/megadose/holehe)** | Given an email, checks 120+ sites for a registered account by probing recovery/signup forms, without alerting the holder. | Emails | No overlap with username tools. |
| **[GHunt](https://github.com/mxrch/GHunt)** | Google-ecosystem OSINT from a Gmail address or GAIA ID: name, photo, Maps reviews, public Photos, YouTube, calendars, device names. Needs cookies from your own Google account. | Google | Google API changes break modules temporarily. |
| **[PhoneInfoga](https://github.com/sundowndev/phoneinfoga)** | Phone-number OSINT: carrier, country, line type, international format, and Internet presence. Web UI + REST API. | Phones | Covers the telephony gap. |

**Pick:** the trio **maigret (usernames) + holehe (emails) + GHunt (Google)**, plus **PhoneInfoga** for phones. social-analyzer only if you need its scoring via API.

---

## 5. Breaches and credentials

| Tool | Description | Notes |
|------|-------------|-------|
| **[h8mail](https://github.com/khast3x/h8mail)** | A CLI for searching emails in breach databases, integrating multiple APIs (Have I Been Pwned, Snusbase, LeakLookup, Hunter.io…) and consolidating results. Bulk input, multiple output formats. | Needs API keys for the services you query. |
| **[Have I Been Pwned (API)](https://haveibeenpwned.com/API/v3)** | Checks whether an email or password has appeared in known breaches. Email queries need a paid key; password queries are free (k-anonymity). | Backend for h8mail. |
| **[Dehashed (API)](https://dehashed.com/)** | Commercial breach database searchable by email, username, IP, real name, phone, postal address and password hash. | The most complete in fields. Paid. |

**Pick:** **h8mail** as the front-end, wired to HIBP (and Dehashed if you pay). Handle leaked credentials responsibly — secure storage, legal basis.

---

## 6. Domains and infrastructure

| Tool | Description | Notes |
|------|-------------|-------|
| **[theHarvester](https://github.com/laramies/theHarvester)** | The classic domain-recon tool: searches engines, DNS, certificate transparency (crt.sh), Shodan, Hunter.io to extract emails, employee names, subdomains, IPs and virtual hosts. Bundled with Kali. | A good starting point. |
| **[amass](https://github.com/owasp-amass/amass)** | OWASP's subdomain-discovery engine. Passive (certs, APIs, archives) + active (brute force, zone transfers). Maps how subdomains relate (ASN, netblocks, registrants) into an attack-surface graph. | More powerful, slower than subfinder. |
| **[subfinder](https://github.com/projectdiscovery/subfinder)** | Fast passive-only subdomain discovery across dozens of sources. Built for pipelines. | The fast sweep; amass for depth. |
| **[Shodan (CLI)](https://github.com/achillean/shodan-python)** | CLI for the search engine of Internet-connected devices: ports, banners, software versions, SSL certs, web screenshots. | Requires API key. Indispensable. |
| **[Censys (CLI)](https://github.com/censys/censys-python)** | Like Shodan but focused on TLS/SSL certificates and HTTPS services; searchable by certificate fields to find infrastructure sharing certs. | Strongest on certificates. |

**Pick:** **subfinder → theHarvester → amass** for the domain map, then **Shodan + Censys** for what is actually exposed.

---

## 7. File and image metadata

Metadata can leak internal usernames, network paths, software versions, dates and GPS coordinates the author never meant to publish.

| Tool | Description | Notes |
|------|-------------|-------|
| **[exiftool](https://github.com/exiftool/exiftool)** | The absolute reference for reading/writing metadata across hundreds of formats (JPEG, PDF, DOCX, MP4…): EXIF, IPTC, XMP, GPS, camera, software, author, dates. Can also strip metadata. | Indispensable. Every OS. |
| **[metagoofil](https://github.com/laramies/metagoofil)** | Finds a domain's public documents via Google, downloads them and extracts metadata: internal usernames, server paths, software versions, emails, printers — passive recon of internal structure. | Excellent passive recon. |
| **[FOCA](https://github.com/ElevenPaths/FOCA)** | GUI document-metadata analysis (ElevenPaths). Like metagoofil but visual; infers internal structure. Windows only. | Windows only. |

**Pick:** **exiftool** for anything file/image-level; add **metagoofil** to harvest a whole domain's documents at once.

---

## 8. Messaging and social networks

| Tool | Description | Notes |
|------|-------------|-------|
| **[Telepathy](https://github.com/jordanwildon/Telepathy)** | The most complete Telegram OSINT toolkit: archives full channel/group messages with metadata, scrapes member lists, analyzes channel activity, maps related channels by forward network, exports reports. | Needs Telegram API credentials (api_id, api_hash). |
| **[Instaloader](https://github.com/instaloader/instaloader)** | A stable, well-maintained Instagram downloader: profiles, photos, videos, stories, highlights, with metadata; private profiles with a session, hashtags, location feeds. | The reliable choice for Instagram. |
| **[snscrape](https://github.com/JustAnotherArchivist/snscrape)** | A no-API social scraper (Reddit, Mastodon, Telegram, VKontakte and historically Twitter/X). | **Largely dead for Twitter/X as of 2026** — X actively blocks this access and the project sees minimal maintenance. Still useful for Reddit/Mastodon. |
| **[Osintgram](https://github.com/Datalux/Osintgram)** | Instagram OSINT with an interactive console (followers, bios, locations, stories). | **Legacy / chronically broken** since 2022-23 due to Instagram changes. Listed for completeness; prefer Instaloader. |

**Pick:** **Telepathy** for Telegram, **Instaloader** for Instagram. For Twitter/X there is no reliable free option now: snscrape is mostly broken — fall back to the **official X API** (paid) or a commercial scraper like **[Apify's Twitter scraper](https://apify.com/apify/twitter-scraper)** when the case justifies it.

---

## 9. Image, facial recognition and photo geolocation

Reverse image search, facial identification and chronolocation (when/where a photo was taken). *(For satellite/aerial imagery itself, see §10.)*

| Tool | Description | Notes |
|------|-------------|-------|
| **[Yandex Images](https://yandex.com/images/)** | The best free reverse image search, especially strong on faces and geographic location; beats Google Images/TinEye at facial matching and finding sources. | Free web. No official public API. |
| **[SunCalc](https://www.suncalc.org/)** | Solar-position calculator for chronolocation: shadows in a photo let you estimate time/date (if location is known) or location (if time is known). | Free web. Essential for chronolocation. |
| **[InsightFace](https://github.com/deepinsight/insightface)** | Open-source deep-learning facial recognition (ArcFace, RetinaFace): build your own reverse face-search against a local corpus instead of a commercial service. | Controlled verification only. GPU recommended. |
| **[DeepFace](https://github.com/serengil/deepface)** | A Python wrapper unifying several facial-recognition models under a simple API: compare faces, search a directory, extract attributes. | Accessible for one-off checks. |
| **[PimEyes](https://pimeyes.com/)** | The most powerful commercial facial search engine — finds other photos of a person across the web. Serious ethical/legal concerns; banned or regulated in places. | Paid. Weigh ethics and legality. |
| **[GeoSpy](https://geospy.ai/)** | Emerging AI that estimates where a photo was taken from visual content alone (no EXIF). | Experimental. Not definitive proof. |

**Pick:** **Yandex Images + SunCalc** are the free workhorses; **InsightFace/DeepFace** for offline face matching. Treat GeoSpy as a hint, not evidence; avoid PimEyes unless the ethics are clearly justified.

> **Verification protocol:** never treat one source as proof. Triangulate — GeoSpy (AI) + SunCalc (shadows) + EXIF (if present) + manual visual analysis (signage, architecture, plates). Reliable only when independent sources converge.

---

## 10. GEOINT — satellite and aerial imagery

Distinct from §9: here you pull and analyze the imagery itself — land use, change over time, infrastructure, terrain.

| Tool | Description | Notes |
|------|-------------|-------|
| **[Copernicus Browser](https://browser.dataspace.copernicus.eu/)** | The free official browser for ESA Sentinel/Copernicus data: true-color, NDVI, SAR, time-series comparison over any area. | Free account. The default starting point. |
| **[Sentinel Hub](https://www.sentinel-hub.com/)** | Web + API access to Sentinel, Landsat and commercial imagery, with custom processing scripts (Evalscript) for automation. | Account/API; free tier limited. |
| **[QGIS](https://qgis.org/)** | The reference open-source GIS to overlay, measure and analyze geospatial layers (imagery, vectors, terrain, your own data). | Free desktop. |

For fresh, very-high-resolution or radar tasking, commercial providers (**Planet**, **Maxar**, **SkyFi**, **ICEYE**) are the option — paid.

**Pick:** **Copernicus Browser** for free Sentinel imagery + **QGIS** to analyze it. Add **Sentinel Hub** when you need an API/automation; commercial tasking only when the free archives are not enough.

---

## 11. Historical web archiving

Recover previous versions of pages and historical URLs — content that was deleted, modified or is gone.

| Tool | Description | Notes |
|------|-------------|-------|
| **[gau (GetAllURLs)](https://github.com/lc/gau)** | Pulls a domain's historical URLs from multiple sources — Wayback Machine, Common Crawl, VirusTotal OTX, AlienVault OTX. | The broadest coverage. |
| **[waybackurls](https://github.com/tomnomnom/waybackurls)** | The same idea, Wayback-only. Fast and simple. | Complementary to gau. |
| **[waybackpy](https://github.com/akamhy/waybackpy)** | Python library for the Wayback Machine API: save/retrieve snapshots, find closest by date, list captures. | For scripts and pipelines. |

**Pick:** **gau** for the widest URL haul, **waybackurls** alongside it, **waybackpy** to script snapshots.

> **Forensic preservation:** for chain of custody, screenshots are not enough. Create Wayback snapshots (public, timestamped) and keep local WARC copies (`wget --warc-file`, `browsertrix-crawler`) that preserve HTTP headers and full content.

---

## 12. Dark web / Tor

Reconnaissance of `.onion` services and hidden content. Keep it compact; always work behind Tor and from an isolated VM.

| Tool | Description | Notes |
|------|-------------|-------|
| **[Ahmia](https://ahmia.fi/)** | A search engine that indexes `.onion` services and is reachable from the clearnet. The cleanest entry point for dark-web search. | Free web. |
| **[OnionSearch](https://github.com/megadose/OnionSearch)** | A CLI that scrapes results across multiple dark-web search engines at once, broadening coverage beyond a single index. | Python; Tor to visit results. |

**Pick:** **Ahmia** to search from the clearnet, **OnionSearch** to broaden across engines. Always behind **Tor** and inside an isolated VM (CSI Linux / tlosint-live / Whonix).

---

## 13. Business intelligence — corporate registries

Ownership, officers and filings. Heavily used in due diligence, investigative journalism and CTI.

| Tool | Description | Notes |
|------|-------------|-------|
| **[OpenCorporates](https://opencorporates.com/)** | The largest open database of companies worldwide — officers, filings and cross-jurisdiction links. | Web + API (key for bulk). |
| **[GLEIF](https://www.gleif.org/)** | The global index of Legal Entity Identifiers (LEI): authoritative entity IDs and parent/child ownership relationships. | Free + API. |
| **[OCCRP Aleph](https://aleph.occrp.org/)** | A searchable archive cross-referencing public records, registries and leaks for investigative work. | Free account. |
| **[Companies House](https://developer.company-information.service.gov.uk/)** | The UK company registry with a free API: officers, filings, charges. | Free (UK only). |

**Pick:** **OpenCorporates** as the cross-border backbone + **GLEIF** for authoritative entity IDs + **Aleph** to cross leaks and registries. Add the national registry for the jurisdiction in scope.

---

## 14. Crypto / blockchain tracing

Following on-chain flows and attributing addresses.

| Tool | Description | Notes |
|------|-------------|-------|
| **[Blockchair](https://blockchair.com/)** | A multi-chain explorer with powerful search and filters across BTC, ETH and many others. | Free + API. |
| **[Etherscan](https://etherscan.io/)** | The reference Ethereum/EVM explorer: transactions, tokens, contracts, address labels. | Free + API. |
| **[Breadcrumbs](https://www.breadcrumbs.app/)** | A visual investigation tool to trace and graph on-chain flows across wallets. | Freemium. |
| **[WalletExplorer](https://www.walletexplorer.com/)** | Bitcoin wallet clustering: groups addresses likely controlled by the same owner. | Free, dated but useful. |

**Pick:** the right explorer for the chain (**Blockchair** multi-chain, **Etherscan** for EVM) + **Breadcrumbs** to visualize flows. Commercial suites (Chainalysis, TRM) only for heavy financial cases.

---

## 15. Aircraft and maritime tracking (SDR / ADS-B / AIS)

Open transponder data, via public platforms or your own software-defined radio.

| Tool | Description | Notes |
|------|-------------|-------|
| **[ADSBExchange](https://www.adsbexchange.com/)** | Unfiltered ADS-B aircraft tracking — shows aircraft that filtered platforms hide. | Free web + API. |
| **[OpenSky Network](https://opensky-network.org/)** | Research-grade aircraft-tracking data with a historical API. | Free (research use). |
| **[MarineTraffic](https://www.marinetraffic.com/)** | The reference AIS platform for vessel positions and history. | Freemium. |
| **[VesselFinder](https://www.vesselfinder.com/)** | An AIS vessel-tracking alternative. | Freemium. |
| **[dump1090](https://github.com/antirez/dump1090)** | A self-hosted SDR decoder to receive ADS-B locally with an RTL-SDR dongle. | Open source; needs hardware. |

**Pick:** **ADSBExchange** (unfiltered) for aircraft, **MarineTraffic** for vessels. OpenSky for historical/API; dump1090 only if you run your own SDR.

---

## 16. Visualization and graph analysis

Graphs surface connections a text investigation hides.

| Tool | Description | Notes |
|------|-------------|-------|
| **[Maltego CE](https://www.maltego.com/)** | The reference platform for entity-graph analysis: build graphs and expand them with "transforms" (automated queries). Community Edition is free but limited; paid editions remove limits. | Commercial transforms need separate subscriptions. |
| **[Gephi](https://github.com/gephi/gephi)** | Open-source network/graph visualization and analysis with metrics (centrality, communities, PageRank) to spot key nodes. | Free. No automated transforms. |

**Pick:** **Maltego CE** when you want transforms (automated expansion); **Gephi** when you just need free, high-quality visualization of data you already have.

---

## 17. Lists and methodology — reference

| Resource | Description |
|----------|-------------|
| **[awesome-osint](https://github.com/jivoi/awesome-osint)** | The large curated reference list (GitHub, Markdown) — the place to look for a tool this catalog does not cover. |
| **Awesome Telegram OSINT** | A curated list specific to Telegram OSINT. |
| **Open-source tools for CTI** | A list of open-source Cyber Threat Intelligence tools (for the defensive/threat-intel adjacent work this catalog deliberately does not cover in depth). |
| **The art of pivoting** | Methodological material on chaining clues from an initial data point to reach what was not directly accessible. |
| **[start.me](https://start.me/)** | A platform for building curated link dashboards, widely used by OSINT practitioners to organize tools and sources into shareable boards. |
| **[OSINT Dashboard](https://github.com/igor-invernon/startme-dashboard)** | A companion to this catalog: 2,000+ OSINT links from leading public start.me collections, unified into one fast, searchable static page. [Live site](https://igor-invernon.github.io/startme-dashboard/). |

**Pick:** keep **awesome-osint** as the master index; use the companion **[OSINT Dashboard](https://igor-invernon.github.io/startme-dashboard/)** for a ready-to-search board of 2,000+ links, and **start.me** to build your own.

---

## Operator OPSEC

Protecting the investigator is part of the workflow. A curated OSINT kit is incomplete without it.

- **Isolation:** run investigations in a disposable VM (tlosint-live, CSI Linux; **Whonix/Tails** for Tor work). Never from your daily-driver OS for adversarial targets.
- **Network:** Tor or a trusted VPN for sensitive queries; never your real/home IP against a target that can look back.
- **Sock puppets:** maintained, non-attributable research accounts — never your real identity. Age them, keep them separate per case.
- **Browser hygiene:** container tabs or separate profiles, block fingerprinting, no cross-login between research and personal accounts.
- **No footprint:** prefer passive tools; avoid actions that notify the target (profile views, follows, likes, password-reset probes on real accounts).

---

## Redundancy analysis — what to use, what to skip

The point of a curated list is to kill noise. Where tools overlap, here is the call.

- **Usernames:** **maigret** is a superset of social-analyzer and simpler utilities. Use maigret; keep social-analyzer only for its scoring via API.
- **All-in-one frameworks:** **spiderfoot** renders older aggregator frameworks nearly redundant. spiderfoot is the engine; **recon-ng** complements it for iterative pivoting.
- **Link directories:** **awesome-osint** (Markdown) beats OSINT Framework (web) for practical use; keep the latter for quick browsing.
- **IOC triage vs. recon:** osint_toolkit (one-off lookups) and spiderfoot (broad crawler) coexist — use each for its job.
- **Instagram:** **Instaloader** (stable) is primary; Osintgram is legacy/broken — do not rely on it.
- **Twitter/X:** no reliable free option in 2026 — snscrape is mostly dead; use the official API or a commercial scraper.
- **Aircraft:** ADSBExchange (unfiltered) over filtered consumer trackers; OpenSky when you need historical/API access.

---

## The shortlist

If you keep only a minimum operational set, keep these:

| Need | Tool(s) |
|------|---------|
| Framework | spiderfoot, recon-ng |
| Identity and accounts | maigret, holehe, GHunt |
| Telephony | PhoneInfoga |
| Messaging | Telepathy, Instaloader |
| Domains and infrastructure | theHarvester, amass, subfinder |
| Breaches | h8mail |
| Metadata | exiftool |
| Exposed devices | Shodan CLI |
| Image and verification | Yandex Images, SunCalc, InsightFace/DeepFace |
| GEOINT (satellite) | Copernicus Browser, QGIS |
| Web archiving | gau, waybackurls, waybackpy |
| Dark web | Ahmia, OnionSearch |
| Corporate registries | OpenCorporates, GLEIF |
| Crypto | Blockchair/Etherscan, Breadcrumbs |
| Aircraft / maritime | ADSBExchange, MarineTraffic |
| Visualization | Maltego CE |
| Reference | awesome-osint |

Everything else is situational — reach for it only when a specific case calls for it.

---

## Coverage map

How complete the OSINT surface is, and where the honest gaps are.

| Area | Status | With |
|------|--------|------|
| People, usernames, emails | Solid | maigret + holehe + GHunt |
| Telegram | Solid | Telepathy |
| Domains and infrastructure | Solid | theHarvester + amass + subfinder + Shodan + Censys |
| Modular framework (console) | Solid | recon-ng |
| Telephony | Solid | PhoneInfoga |
| Credential breaches | Solid | h8mail + HIBP + Dehashed |
| File metadata | Solid | exiftool + metagoofil + FOCA |
| Exposed devices and services | Solid | Shodan + Censys |
| GEOINT (satellite/aerial) | Solid | Copernicus Browser + Sentinel Hub + QGIS |
| Historical web archiving | Solid | gau + waybackurls + waybackpy |
| Dark web / Tor | Covered (compact) | Ahmia + OnionSearch |
| Corporate registries / BI | Solid | OpenCorporates + GLEIF + Aleph + Companies House |
| Crypto / blockchain | Solid | Blockchair + Etherscan + Breadcrumbs |
| Aircraft / maritime | Solid | ADSBExchange + OpenSky + MarineTraffic |
| Graph visualization | Solid | Maltego CE + Gephi |
| Image and faces | Partial | Yandex + InsightFace/DeepFace (open source); PimEyes (commercial, ethically risky) |
| Photo geolocation | Partial | GeoSpy (experimental) + SunCalc + manual verification |
| Instagram | Conditional | Instaloader stable; Osintgram legacy/broken |
| Twitter/X | Weak | No reliable free option in 2026; official API or commercial scraper |

---

## Operational playbooks

Recommended tool sequences for common cases. Each step's output feeds the next. The **weak link** note flags the most fragile step and its fallback.

### Domain reconnaissance (fast)

```
subfinder (passive subdomains, fast)
  -> theHarvester (emails, hosts, corporate addresses)
    -> Shodan/Censys (services exposed per IP)
      -> amass (deeper: ASN relationships, netblocks, registrants)
        -> spiderfoot scan (full automatic correlation)
```
*Weak link:* third-party API keys (Shodan/Censys quotas). Fallback: amass/subfinder run on public sources without keys, just with less coverage.

### Person identification (username/email)

```
maigret (username enumeration across thousands of sites)
  -> holehe (email verification against 120+ services)
    -> GHunt (if the email is Gmail: Google ecosystem)
      -> h8mail / Dehashed (breach checking)
        -> PhoneInfoga (if a phone number turns up)
```
*Weak link:* GHunt (Google API changes break it). Fallback: skip to breach/identity pivots; re-run GHunt after an upstream fix.

### Telegram channel investigation

```
Telepathy (message archive, member list, activity analysis)
  -> extract usernames/emails/phones of members
    -> maigret + holehe (pivot on found identities)
      -> Maltego CE (relationship-graph visualization)
```
*Weak link:* Telepathy (Telegram API changes / rate limits). Fallback: the public web view `t.me/s/<channel>` for read-only scraping of public channels.

### Image / geolocation verification

```
exiftool (EXIF: GPS, camera, software, dates)
  -> Yandex Images (reverse search: source, other appearances)
    -> InsightFace/DeepFace (facial verification if faces present)
      -> GeoSpy (AI location estimate) + Copernicus Browser (satellite context)
        -> SunCalc (shadow triangulation if time/date known)
          -> manual visual analysis (signage, architecture, plates)
```
*Weak link:* GeoSpy (experimental, low confidence). Fallback: rely on SunCalc + manual analysis; treat GeoSpy as a hint only.

### Corporate due diligence

```
OpenCorporates (entity, officers, jurisdictions)
  -> GLEIF (LEI, parent/child ownership)
    -> national registry (Companies House etc.: filings, charges)
      -> Aleph (cross-reference leaks and records)
        -> Maltego CE (map the ownership graph)
```
*Weak link:* coverage varies by country. Fallback: go straight to the national registry for jurisdictions OpenCorporates indexes poorly.

---

## Credentials and quotas

Several tools need API keys. Pricing changes often, so this links to each service's pricing page rather than hardcoding figures.

| Tool | Service | Key needed? | Pricing |
|------|---------|-------------|---------|
| spiderfoot | Multiple (Shodan, VirusTotal, HIBP, SecurityTrails…) | Optional | Works on public sources; keys unlock more. |
| h8mail | HIBP, Snusbase, LeakLookup, Hunter.io | Yes (per backend) | HIBP needs a paid key for email lookups. |
| Shodan CLI | Shodan | Yes | [shodan.io/pricing](https://account.shodan.io/billing) |
| Censys CLI | Censys | Yes | [censys.io/pricing](https://censys.io/pricing) |
| Dehashed | Dehashed | Yes | [dehashed.com](https://dehashed.com/) |
| GHunt | Google (session cookies) | Cookies | Free |
| Telepathy | Telegram API | Yes | Free — [my.telegram.org](https://my.telegram.org/) |
| Sentinel Hub | Copernicus Data Space | Optional | [dataspace.copernicus.eu](https://dataspace.copernicus.eu/) |
| OpenCorporates | OpenCorporates API | For bulk | [opencorporates.com/api_accounts/new](https://opencorporates.com/api_accounts/new) |

Keep keys out of cleartext in any repository: use a GPG-encrypted `.env` (ship a `.env.example`), or a secrets manager, and store CI keys in the platform's secret store.

---

## Legal and ethical considerations

That information is technically accessible does not make it legal or ethical to collect, store or use. OSINT lives in that gap.

### Risks by jurisdiction

| Framework | Applies to | Impact on OSINT |
|-----------|-----------|-----------------|
| GDPR (EU/EEA) | Personal data of EU residents | Collecting/storing/processing personal data without a legal basis can incur penalties. Especially affects people-enumeration tools (maigret, holehe, GHunt). |
| EU AI Act | AI systems in the EU | Phasing in from 2025. Remote biometric identification / facial recognition (PimEyes, and self-hosted InsightFace/DeepFace used this way) is classed high-risk or restricted. Check obligations before any face-matching at scale. |
| PIPEDA (Canada) | Personal data, commercial context | Requires a documented legitimate purpose. |
| CCPA/CPRA (California) | Personal data of California residents | Access, deletion and opt-out rights. |
| CFAA (USA) | Access to computer systems | Scraping can be read as "unauthorized access" under recent case law. Mind tools hitting undocumented APIs (Osintgram, snscrape). |
| Facial-recognition laws | Varies | PimEyes banned/regulated in several places; Illinois (BIPA) requires consent for biometric capture. |

### Responsible-use checklist

1. **Legitimate purpose** — a documented lawful reason (journalism, corporate security, legal defense, missing persons, academic research).
2. **Proportionality** — methods match the goal; no mass facial recognition for a fact a simple search would give.
3. **Data minimization** — collect only what the objective needs.
4. **Secure storage** — encrypted, access-restricted, with a retention/deletion policy.
5. **No contact** — tools must not alert or contact the subject (holehe and GHunt are built for this).
6. **Documentation** — record tools, timestamps, parameters and results, for chain of custody.

---

## Machine-readable companion

This Markdown catalog is for humans; `tools.json` and `tools.csv` hold the same catalog in structured form for filtering, reporting and automation.

Fields per record: `name`, `category`, `tags`, `short_desc`, `url`, `language`, `interface`, `requires_api_keys`, `license`, `last_commit_date`, `maintenance_status`, `recommended_role` (core / backup / conditional / experimental / archive), `risk_notes`, `install_hint`.

Example — list the core tools per category with `jq`:

```bash
jq -r '.[] | select(.recommended_role=="core") | "\(.category)\t\(.name)"' tools.json
```

Or filter to actively maintained tools in Python:

```python
import json
tools = json.load(open("tools.json"))
active = [t for t in tools if t.get("maintenance_status") == "active"]
```

> **Data freshness:** `last_commit_date` and `maintenance_status` were verified as of **2026-05-29** and require periodic manual review — treat them as a snapshot, not live state.
