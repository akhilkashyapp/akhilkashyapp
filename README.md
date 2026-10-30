<p align="center">
  <img src="assets/banner.svg" width="100%" alt="Akhil Kashyap, AI engineer, freight">
</p>

I build the software that runs a freight brokerage at Fords Fast Freight. Loads get posted, carriers get answered, rates get negotiated, trucks get tracked and the TMS stays current, with people stepping in where judgment is needed. Most of it runs in production every day.

<p align="center">
  <img src="assets/lifecycle.svg" width="100%" alt="One load, end to end: post, quote, negotiate, dispatch, track, deliver, learn">
</p>

#### Systems

| | |
|---|---|
| **Load posting** | Posts loads to the DAT load board from a Teams command, by load, in bulk or for a whole pod. Certified by DAT for production load posting. Keeps live postings refreshed and records metrics per load. |
| **Carrier inbound** | Owns the dispatch mailbox. Classifies carrier email, works out which load is being asked about and replies with the details. Negotiates rate over multiple turns inside limits the broker sets. Its rules are pinned by a regression suite built from real incidents. |
| **Track and trace** | Opens the tracking thread the moment a rate confirmation is signed and follows the load to delivery on a status-driven cadence. One instance per operating pod, each with its own mailbox and database. |
| **Check calls** | Voice calls to drivers and dispatchers for location and ETA, with SMS fallback. Separately, live FourKites coordinates every 30 minutes, dropped on the load in the TMS as map markers. |
| **Market data** | Polls the major US freight markets on DAT every 15 minutes for van and reefer: loads, trucks, the ratio between them and posted rates. Markets are our own, built from 3-digit ZIP groupings. |
| **Market intelligence** | Reads freight news, the calendar and the weather, and flags what is about to move the market before it shows on the board. |
| **Data spine** | Every load from the TMS into Postgres: lane, both sides of the rate, every stop and charge line. Read-only. The base for rate prediction and a company-wide carrier CRM. |
| **Control plane** | One dashboard for the company. Microsoft sign-in, invite only, scoped per pod. Every agent visible, switchable, and queryable through a read-only assistant. |

#### How I build

```
one service per agent      own repo, own deploy, own database
read-only first            write access after a dry run and a human review
incidents become tests     every production failure is pinned so it stays fixed
pods are isolated          one team's configuration cannot break another's
```

#### Stack

```
languages       Python, SQL, PHP
services        FastAPI, asyncio, APScheduler, Postgres
ai              Claude (Anthropic API), LangGraph, LangChain, Deepgram
integrations    DAT, AscendTMS, FourKites, Microsoft Graph, Entra ID, Teams, Vonage
infra           Railway, Docker, GitHub
```

<p align="center">
  <a href="https://www.linkedin.com/in/kashyapakhil25/">LinkedIn</a>
</p>
