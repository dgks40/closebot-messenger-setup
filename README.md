# gohighlevel facebook messenger bot: how to connect Messenger, get an AI agent replying in seconds, and actually book appointments

Most people searching for a GoHighLevel Facebook Messenger bot are trying to solve one of two problems, and they're not the same problem.

Problem one: messages from a Facebook Page sit somewhere outside the CRM, and nobody wants to answer them manually at 11pm. Problem two: messages already land in the GoHighLevel Conversations inbox, but the replies are slow, generic, or stop after two exchanges because the bot can't hold a real conversation.

Which one you have decides what you actually need to buy. So let's untangle the layers first, then walk through the setup, then look at pricing honestly.

## The GoHighLevel Facebook Messenger bot is two separate things stacked on top of each other

There's no single product called "a GoHighLevel Facebook Messenger bot." There's a channel connection and a brain.

**The channel connection** is GoHighLevel's. The platform connects a Facebook Page plus a linked Instagram account to a sub-account, and from that moment every Messenger DM and Instagram DM shows up as a conversation with a contact inside the CRM. That part is native, and it's free with your GoHighLevel subscription.

**The brain** is whatever answers those messages. GoHighLevel ships its own (Conversation AI). You can also run a third-party agent that watches the same Conversations inbox and replies instead.

CloseBot sits in that second category. It's worth being precise about this because it's the single most misunderstood thing about the product: CloseBot does not connect to Facebook Messenger itself. It connects to your CRM and takes over the text conversations already flowing there. CloseBot's own documentation puts it plainly — it "piggy-backs off of any channel that your CRM supports," so once a Messenger message lands as a GoHighLevel conversation, the agent can answer it.

If you expected a tool that plugs straight into a Facebook Page and skips the CRM, that's a different category of product. If your leads already run through GoHighLevel, this architecture is exactly what you want.

## Step 1: Get Facebook Messenger (and Instagram) into GoHighLevel

Do this before you shop for any AI layer, because nothing downstream works until the messages are visible in the CRM.

1. In the sub-account, go to **Settings → Integrations**.
2. Click **Connect** under Facebook & Instagram.
3. Log in to Facebook and pick the Page you want. Critically, pick the Page that's already linked to your Instagram business or creator account — linking them later is an extra step and a common source of missing DMs.
4. Approve **Connect Facebook & Instagram**.
5. Click **Sync Leads**.

Then test it properly. The GoHighLevel help doc is specific about this: send the test message from a *different* Facebook or Instagram account, not the business account you connected. A message sent from your own admin account can behave differently, and you'll end up debugging a connection that was fine.

The test passes when the message appears in **Conversations** under the right contact, and when your reply from inside GoHighLevel arrives back in Messenger. Missing messages are almost always one of three things: the wrong Page got connected, Instagram isn't linked to that Page at all, or messaging permissions weren't fully granted during OAuth.

One more note that matters for qualification: when someone messages you for the first time, GoHighLevel creates or updates a contact based on your Contact Deduplication Preferences. If you allow duplicate contacts, you can end up with the same person existing as two records — one from Messenger, one from a form fill. That quietly breaks lead routing and reporting later, so fix it before you scale ad spend.

## Step 2: Choose what answers the messages

### What GoHighLevel's native Conversation AI does

Conversation AI is genuinely capable for straightforward work. The official docs list support for SMS, email, Facebook, Instagram, WhatsApp, chat widget, and live chat, with lead capture, appointment booking, and handover to a human. You've got three setup paths: a guided form for simple cases, a prompt-based bot if you're comfortable writing instructions, and a flow builder for branching logic.

There's a sensible way to run it, too: keep the bot in **Suggestive** mode and review its drafts before switching to **Auto-Pilot**. Bots default to Off for a reason.

### Where the native bot tends to run out of road

The friction shows up in specific places:

- **One primary bot per sub-account.** GoHighLevel's own documentation describes assigning one primary bot to handle general inbound messages on selected channels. If your Facebook Messenger traffic includes two very different lead types (say, buyers and sellers), you're working around that constraint.
- **Prompt-driven behavior.** The bot follows instructions rather than an explicit multi-step structure, which makes complex qualification sequences harder to control.
- **Channel-level automation quirks.** Community threads describe cases where the provider switches mid-conversation, and the ideas board has a long-standing request that Conversational AI should pause when a human replies from the native Instagram or Messenger app.
- **Cost at agency scale.** GoHighLevel's own pricing for AI Employee is a flat per-sub-account fee, or roughly $0.02 per conversation message on the pay-as-you-go path. Those two paths scale very differently. We'll do the math below.
- **Facebook Marketplace doesn't come along for the ride.** Anything happening in personal Messenger, including Marketplace chats, isn't pullable into GoHighLevel the way Page DMs are.

None of that makes Conversation AI bad. It makes it a generalist feature inside a very large platform, which is roughly what CloseBot's comparison blog argues — with an obvious commercial interest in saying so, and you should read it in that light.

## Where CloseBot fits on top of your Messenger inbox

CloseBot is the AI layer, and your CRM is the plumbing. The workflow looks like this: a lead DMs your Facebook Page, GoHighLevel creates the contact, CloseBot's agent picks up the conversation, qualifies against your criteria, updates custom fields, and books straight onto a GoHighLevel calendar — often without a booking link ever being sent.

Practical details worth knowing before you commit:

**You can restrict which channels an agent answers.** Source Filters let you scope an agent to specific channels, so a Messenger-specific agent and an SMS agent can coexist without stepping on each other.

**Multiple agents per sub-account are allowed.** Unlike the one-primary-bot model, you can have different agents listening based on channel or tags.

**Quiet hours are configurable per channel.** CloseBot supports different reply windows for different messaging channels, so Messenger can run 24/7 while SMS respects legal sending hours.

**It reads images.** A lead screenshots something and sends it; the agent can see it. In home services and real estate this comes up constantly.

**Booking failures get retried.** Calendar errors don't immediately turn into "sorry, that slot is taken" — the agent tries again, which CloseBot attributes to a meaningful lift in booked appointments.

**Unanswered questions surface instead of being invented.** There's a smart FAQ that flags you when the agent isn't confident, plus provider fallback across OpenAI, Anthropic, Gemini, Grok, and DeepSeek if one model goes down.

If you want to see the agent running against your own Messenger traffic rather than a demo, 👉 [start a free CloseBot account and connect your GoHighLevel sub-account](https://app.closebot.com/a?fpr=li87) — the free tier is capped at 100 messages a month, which is enough to test on live conversations before spending anything.

## CloseBot setup: from zero to a live Messenger agent

The company markets a 48-second setup, which refers to registering and connecting a source. Realistically, a production agent takes longer, but the sequence itself is short:

1. **Create the account.** Pick your industry during signup — CloseBot auto-creates a starter agent with a basic Q&A profile.
2. **Add a source.** Open **Sources → New Source**, choose HighLevel or LeadConnector, and approve the OAuth window for the right sub-account.
3. **Tick "Allow CloseBot to create/update fields."** Skip this and your agent can read conversations but can't write qualification data back to the CRM — which defeats half the point.
4. **Connect the source to the agent.** Your starter agent is already there; point it at the new source.
5. **Build the job flow.** This is the real work. Drag in qualification steps, define disqualification criteria, and add a booking node connected to your GoHighLevel calendar. A persona keeps the tone consistent with the client's brand.
6. **Set follow-up and operating hours.** Follow-ups should fire during business hours only, and per-channel reply windows matter if Messenger and SMS share an agent.
7. **Test before going live.** Run a real conversation from a personal Facebook account into the Page, check the custom fields populated correctly, then book and cancel an appointment to confirm the calendar logic.

Two things to plan for: your own model API keys (CloseBot requires them rather than bundling model costs), and someone who will actually supervise the agent for the first couple of weeks. Agents that set appointments well still need a human reviewing transcripts early on.

## CloseBot pricing: every plan currently on the page

Here's the full picture from CloseBot's plans page. Business plans bundle message costs into the base price; the Agency plan meters messages and lets you rebill them.

| Plan | Who it's for | What's included | Price | Billing | Get started |
| --- | --- | --- | --- | --- | --- |
| **Free** | Testing CloseBot or very low lead volume | 100 messages/month, 1 agent, 1 user seat, 1 MB storage, unlimited account connections | $0 | Always free (overage $0.08/message) | [Open the free plan](https://app.closebot.com/a?fpr=li87) |
| **Core (Business)** | Businesses qualifying and booking their own leads | Message costs included, 500 messages/month at base, 15+ templates, human support, add additional seats/storage/agents | $64/mo (annual: $53/mo, billed as $640/yr) | Monthly or annual, 7-day trial | [Start the Business Core trial](https://app.closebot.com/a?fpr=li87) |
| **Core (Agency)** | Agencies building and rebilling AI agents for clients | Unlimited agents and sources, white-label client portal, rebill all costs, flat per-message rate you can mark up | $397/mo | Monthly, 7-day trial | [Start the Agency Core trial](https://app.closebot.com/a?fpr=li87) |
| **Growth** | Teams needing SLAs, compliance, or high volume | HIPAA compliance, quarterly audits, 99.99% priority uptime, priority support, 50+ templates | Custom | Quote-based | [Request Growth pricing](https://app.closebot.com/a?fpr=li87) |

A few points that don't fit neatly into a table:

- **Message volume is a slider on business plans.** The $64 base covers 500 messages. Raising the monthly ceiling lowers your effective per-message rate; going over the ceiling costs a 2x overage drawn from your wallet.
- **Annual billing effectively gives you two months free**, and it also unlocks the larger 50+ template library.
- **Add-ons are separate.** Extra user seats run $5 each. Business storage is included at 1 MB with paid tiers above that; agency storage is billed daily per MB.
- **There are no refunds**, but there is a free-forever tier under 100 messages and a 7-day trial on any paid plan. Plans are month-to-month with no contract, so downgrading is possible.
- **You can't bring your own API key to cut costs** — CloseBot frames this as a security decision, and it means model spend is baked into your plan. Note that token costs for your AI provider are still yours on top of the plan.

One inconsistency worth flagging: the plans page FAQ currently lists the agency per-message rate at $0.012, while CloseBot's older support articles cite $0.006. Check the current figure inside your account before you build a client pricing model around it.

## The cost stack nobody mentions: Messenger bots run on a CRM

This is where a lot of people get surprised. CloseBot is the AI layer; GoHighLevel is still a separate subscription. Current GoHighLevel pricing runs $97/month for Agency Starter, $297/month for Agency Unlimited, and $497/month for Agency Pro.

So a business that wants roughly 1,000 Messenger messages a month handled well is looking at a CloseBot business plan plus a GoHighLevel plan, before any per-message usage above the ceiling. That's not an argument against either product — it's just the honest total cost of ownership, and it's the reason people sometimes end up deciding a CRM-plus-agent stack is more than their volume justifies.

CloseBot's own blog ran the comparison from their side of the fence, and the numbers are still useful as an illustration of how the two pricing models diverge at scale. In their example of a 102-sub-account agency sending about 24,720 messages a month, GoHighLevel's AI Employee route came out at $97 × 102 sub-accounts, while the pay-per-use Conversational AI route came out around $0.02 per message. Their conclusion — that a flat per-sub-account fee gets painful for an agency with many small clients — is arithmetic rather than marketing. Just remember the source.

## What people who actually use these tools say

Reviews split along architecture, not quality.

On G2, CloseBot's reviewers consistently point to ease of use and quick setup as the standout, along with the ability to automate conversations without hand-holding. In GoHighLevel and automation subreddits, the recurring line is that people prefer it to the native chat AI for conversational appointment booking and rescheduling — comments like "way better than GHL chat AI" show up repeatedly, though so does the counterpoint that the learning curve put some users off entirely.

A third-party review that verified pricing in August 2026 makes the most useful distinction: CloseBot is a strong agent, but it's built to live inside a CRM. If you run GoHighLevel with Messenger connected, that's a feature. If you don't run a CRM at all, you'd be buying two products to solve one problem.

That's the correct framing. The product quality isn't in question; the fit is.

## Messenger bot problems you'll hit, and what actually causes them

**DMs don't appear in the CRM.** Wrong Page connected, or Instagram isn't linked to the Page. Go back to Settings → Integrations and confirm both.

**The test message worked, real messages don't.** Duplicate contacts or a deduplication setting splitting the person into two records. Check Contact Deduplication Preferences.

**The agent stops replying mid-conversation.** Usually a filter, a channel restriction, or a bot handoff where two agents were both eligible. Source Filters make this easy to misconfigure.

**The agent replies to a thumbs-up with a sales pitch.** Emoji reactions shouldn't trigger a response; this is a known failure mode in cheaper tools and something to test explicitly during your trial.

**Marketplace messages never arrive.** Personal Messenger and Marketplace chats aren't available to GoHighLevel. Only Page-based conversations are.

## So which setup do you actually want?

**Use GoHighLevel's native Conversation AI if** your conversations are simple inbound questions, your volume is modest, and you want one vendor and one bill. Start in Suggestive mode, review the drafts, and only then switch to Auto-Pilot.

**Add CloseBot if** Messenger is a real lead source and the conversations need to qualify and book, not just answer. The strongest cases are agencies reselling AI under their own brand with rebilling, businesses running complex multi-step qualification, and industries like home services and real estate where image reading, drive-time checks, and property tools genuinely change outcomes.

**Prototype on the free tier regardless.** One hundred messages a month costs nothing and tells you more than any demo. 👉 [Test a CloseBot agent on your own Messenger conversations](https://app.closebot.com/a?fpr=li87) before you commit to a monthly plan.

## FAQ

**Does CloseBot connect directly to Facebook Messenger?**
No. It connects to GoHighLevel, HubSpot, LeadConnector, or a custom CRM via webhook, and answers the channels connected there. Messenger works because GoHighLevel's Facebook integration puts those DMs into the Conversations inbox.

**Which channels can a single CloseBot agent cover?**
Whatever your CRM supports — SMS, email, live chat, WhatsApp, Facebook Messenger, Instagram DMs, or a custom channel provider. Not every channel needs the same agent; you can split by channel or tag.

**Does it book appointments directly in Messenger?**
Yes, if you add a booking node connected to a calendar. The agent checks availability and confirms in the conversation instead of sending a booking link.

**How many messages does the free plan allow?**
100 per month, forever, with 1 agent, 1 user seat, and 1 MB of storage. Overages run $0.08 per message if you'd rather pay than upgrade.

**Is there a refund if it doesn't work out?**
No refunds. Instead there's a free plan and a 7-day trial on any paid plan, with month-to-month terms so cancelling is straightforward.

**What's the total monthly cost for a small business?**
A CloseBot business plan from $64/month plus a GoHighLevel plan from $97/month, roughly. Add WhatsApp fees and any message overage above your ceiling.

The short version: GoHighLevel gets Messenger into the building. Something else has to answer it well. Decide which of those two jobs is actually failing for you, and you'll know whether you need a channel fix or a better brain.
