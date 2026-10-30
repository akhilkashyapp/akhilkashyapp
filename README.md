### Akhil Kashyap

AI engineer at Fords Fast Freight.

I build the systems that run a freight brokerage: agents that post loads, answer carriers, negotiate rates, track trucks and keep the TMS current. Most of what follows runs in production.

---

#### Systems

**Load posting**
Posts loads to the DAT load board from a Teams command, by load, in bulk, or for a whole pod. Certified by DAT for production load posting. Refreshes live postings and records metrics per load.

**Carrier inbound and negotiation**
Owns the dispatch mailbox. Classifies inbound carrier email, works out which load is being asked about, replies with the details and negotiates rate over multiple turns inside limits the broker sets. Checks the carrier's authority before quoting. Its rules are pinned by a regression suite built from real incidents.

**Track and trace**
Opens the tracking thread the moment a rate confirmation is signed and follows the load through delivery on a status-driven cadence. Runs as a separate instance per operating pod, each with its own mailbox and database.

**Voice check calls**
Calls drivers and dispatchers for location and ETA, falls back to SMS, and writes the answer into the TMS. Every attempt is logged, including voicemail and no answer.

**GPS check calls**
Pulls live coordinates from FourKites every 30 minutes and drops them on the load in AscendTMS as map markers.

**Market data**
Polls the major US freight markets on DAT every 15 minutes for van and reefer: posted loads, posted trucks, the ratio between them and the advertised rates. Every reading is kept. Markets are our own, defined from 3-digit ZIP groupings.

**Market intelligence**
Reads freight news, the calendar and the weather, and flags what is about to move the market before it shows up on the board.

**Data spine**
Ingests every load from AscendTMS into Postgres: lane, both sides of the rate, every stop and every charge line. Read-only by design. It is the training set for rate prediction and the base of a company-wide carrier CRM.

**Mailbox automation**
Reads Microsoft 365 inboxes, including OCR on scanned PDF attachments, and files what Outlook rules cannot see.

**Control plane**
One dashboard for the company. Microsoft sign-in, invite only, scoped per pod. Shows every agent, lets operators switch them on and off, and includes a read-only assistant that answers questions over the same data.

---

#### How I build

- One service per agent. Own repo, own deploy, own database.
- Read-only first. Write access comes after a dry run and a human review of the output.
- Every production incident becomes a test.
- Pods are isolated, so one team's configuration cannot break another's.

---

#### Stack

```
Languages      Python, SQL, PHP
Services       FastAPI, asyncio, APScheduler, Postgres
AI             Claude (Anthropic API), LangGraph, LangChain, Deepgram
Integrations   DAT, AscendTMS, FourKites, Microsoft Graph, Entra ID, Teams, Vonage
Infra          Railway, Docker, GitHub
```

---

#### Contact

[LinkedIn](https://www.linkedin.com/in/kashyapakhil25/)
