<p align="center">
  <img src="images/banner.svg" alt="ContractHub: contract lifecycle management on Microsoft Power Platform" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Power%20Apps-Canvas-742774?style=for-the-badge" alt="Power Apps">
  <img src="https://img.shields.io/badge/Dataverse-8%20tables-038387?style=for-the-badge" alt="Dataverse">
  <img src="https://img.shields.io/badge/Power%20Automate-3%20flows-0066FF?style=for-the-badge" alt="Power Automate">
  <img src="https://img.shields.io/badge/Power%20Fx-UDFs-CA5010?style=for-the-badge" alt="Power Fx">
  <img src="https://img.shields.io/badge/ALM-Solution--aware-107C10?style=for-the-badge" alt="ALM">
</p>

<p align="center">
  <b>ContractHub</b> is a contract management solution built end-to-end on <b>Power Apps</b>, <b>Dataverse</b> and
  <b>Power Automate</b>. It takes a contract from draft through review, multi-stage approval, activation and renewal.
  Approvers get modern HTML emails with a generated PDF summary and a one-click link back into the app.
</p>

![ContractHub dashboard](images/dashboard.png)

---

## ✨ Highlights

<table>
  <tr>
    <td width="33%" valign="top">
      <h3>🔄 Full lifecycle</h3>
      Draft → In Review → Pending Approval → Approved → Active → Renewed / Expired / Terminated, with a one-click "Move to next stage".
    </td>
    <td width="33%" valign="top">
      <h3>🧭 Approval routes</h3>
      Approvers per stage, with a default route per contract type that any contract can override.
    </td>
    <td width="33%" valign="top">
      <h3>✅ Automated approvals</h3>
      The last approval advances the contract. A rejection sends it back one stage with the approver's comment.
    </td>
  </tr>
  <tr>
    <td width="33%" valign="top">
      <h3>📧 Branded emails</h3>
      Responsive HTML with a lifecycle tracker, approval trail, recent activity and a deep link into the app.
    </td>
    <td width="33%" valign="top">
      <h3>📄 PDF summary</h3>
      Generated on the fly and attached to every email, together with the latest signed contract document.
    </td>
    <td width="33%" valign="top">
      <h3>🕓 History timeline</h3>
      Comments, calls, negotiations, stage changes, decisions, milestones and documents, newest first.
    </td>
  </tr>
</table>

---

## 📊 Dashboard & contracts

A live view of the portfolio: active contract value, contracts expiring in 60 days, overdue milestones,
and contracts by status. The contract list supports search and quick filters.

![Contracts list](images/contracts.png)

## 📁 Contract workspace

Each contract opens in a workspace with KPI cards, a **lifecycle stepper** and tabs for **Overview, History,
Milestones, Approvals and Documents**.

![Contract details](images/contract-details.png)

| 🕓 History timeline | 🎯 Milestones |
|---|---|
| ![History](images/contract-history.png) | ![Milestones](images/contract-milestones.png) |

## 🧭 Approval routing

> [!TIP]
> Admins set up a **default approval route** for each contract type, with approvers for
> **In Review**, **Pending Approval** and **Final Sign-off**. Any contract can customise its own route on its Approvals tab.

![Approval routes](images/approval-routes.png)

When a contract enters a stage, the app creates an approval request for each approver on that stage's route.
The assigned approver sees a **"Your decision is needed"** panel and decides in one click.

| ✅ Decision on a contract | 📥 Approvals inbox |
|---|---|
| ![Approval decision](images/approval-decision.png) | ![Approvals](images/approvals.png) |

> [!IMPORTANT]
> **The last approval of a stage moves the contract forward automatically.** A **rejection** needs a comment,
> withdraws the other open requests and sends the contract back one stage.

## 📧 Email notifications & PDF

Three Power Automate flows keep everyone informed:

<table>
  <tr><th align="left">Flow</th><th align="left">Trigger</th><th align="left">Recipient</th></tr>
  <tr><td><img src="https://img.shields.io/badge/Approval%20request-D4A24C?style=flat-square" alt="Approval request"></td><td>An approval is requested for a stage</td><td>👤 Approver</td></tr>
  <tr><td><img src="https://img.shields.io/badge/Approval%20decision-2E9E6B?style=flat-square" alt="Approval decision"></td><td>An approver approves or rejects</td><td>👤 Contract owner</td></tr>
  <tr><td><img src="https://img.shields.io/badge/Status%20change-0F6E64?style=flat-square" alt="Status change"></td><td>The contract moves to a new stage</td><td>👤 Contract owner</td></tr>
</table>

Every email includes key terms, a lifecycle tracker, the approval trail, recent activity and a
**Review & decide** button that opens the contract directly in the app. The attachments are a generated
**PDF contract summary** and the latest uploaded contract document.

| 📧 Approval email | 📄 Generated PDF summary |
|---|---|
| ![Approval email](images/email-approval-request.png) | ![PDF summary](images/contract-summary-pdf.png) |

## 🤝 Parties & milestones

| 🏢 Parties | 🎯 Milestones across all contracts |
|---|---|
| ![Parties](images/parties.png) | ![Milestones](images/milestones.png) |

---

## 🏗️ Architecture

```mermaid
flowchart LR
    A["Power Apps canvas app<br/>9 screens · Power Fx UDFs"] -- read / write --> B[("Dataverse<br/>8 tables")]
    B -- row created / updated --> C["Power Automate<br/>3 flows"]
    C -- HTML → PDF --> D["OneDrive"]
    C -- HTML email + PDF --> E["Outlook"]
    E -- "Review & decide" deep link --> A
```

<table>
  <tr>
    <td width="50%" valign="top">
      <h3>🗃️ Data model</h3>
      <img src="https://img.shields.io/badge/Contract-13203A?style=flat-square" alt="Contract">
      <img src="https://img.shields.io/badge/Party-13203A?style=flat-square" alt="Party">
      <img src="https://img.shields.io/badge/Contract%20Type-13203A?style=flat-square" alt="Contract Type">
      <img src="https://img.shields.io/badge/Milestone-0F6E64?style=flat-square" alt="Milestone">
      <img src="https://img.shields.io/badge/Document-0F6E64?style=flat-square" alt="Document">
      <img src="https://img.shields.io/badge/Comment-0F6E64?style=flat-square" alt="Comment">
      <img src="https://img.shields.io/badge/Approval-D4A24C?style=flat-square" alt="Approval">
      <img src="https://img.shields.io/badge/Stage%20Approver-D4A24C?style=flat-square" alt="Stage Approver">
    </td>
    <td width="50%" valign="top">
      <h3>⚙️ Engineering notes</h3>
      <ul>
        <li>Approval logic lives in Power Fx <b>user-defined functions</b>, shared by every screen</li>
        <li><b>Delegation-safe</b> Dataverse queries, with no delegation warnings</li>
        <li>Email and PDF templates are <b>generated from source</b>, so they're versioned and previewable</li>
        <li>Everything ships in <b>one solution</b>, with environment variables and connection references</li>
      </ul>
    </td>
  </tr>
</table>

---

<p align="center">
  <b>Designed and built by Muhammad Bilal</b>, Power Platform developer<br>
  <sub>I build business apps, approval workflows and automations with Power Apps, Dataverse and Power Automate.<br>
  Get in touch to discuss a similar solution for your team.</sub>
</p>
