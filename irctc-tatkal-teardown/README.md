# Tatkal: The Opening Rush — a product teardown

**By Sriram A · November 2026**
Product Manager, digital lending · [LinkedIn](https://www.linkedin.com/in/sriram-aramuthan)

> Built from public information only. Views are my own; no affiliation with IRCTC or Indian Railways.

**Carousel:** [`tatkal-teardown.pdf`](./tatkal-teardown.pdf) (8 slides)

---

## TL;DR

You're logged in at 9:59, passengers saved, wallet topped up, and you still miss the ticket. To the user every miss looks the same. Underneath, there are three different problems: **the system failed** while seats were still there, **the quota sold out** before your turn, or **the status is unclear** (charged, but no PNR). Each one needs a different fix.

**My approach:**

1. **Diagnose first.** Tag every attempt with one outcome: PNR / system failure / quota gone / payment pending.
2. **Then fix it with a queue and a seat hold.** A waiting room from 9:45 that admits people only as fast as the system can book, uses the wait to get passengers and wallet ready, holds your berth for a time set by your payment method, and hands it to the next person in the queue if payment fails, with an automatic refund.

---

## 1. The journey: five stops to a PNR

Tatkal opens one day before the journey: 10:00 AM for AC classes, 11:00 AM for non-AC. Each step can break under load.

| Step | What goes wrong |
| --- | --- |
| Sign in | OTP is late, the page times out, the session expires |
| Check availability | AVAILABLE turns to WL in the seconds it takes to click |
| Confirm passengers | The form hangs, or a validation error resets it |
| Pay | Money is debited, the screen says failed, or shows nothing |
| Get an outcome | PNR, sold out or pending? Users usually can't tell |

Any failure sends the user back to the start, and every retry adds load at the worst possible second.

## 2. The scale, and why it isn't the diagnosis

- Bots made up as much as **half of login attempts** in the first five minutes of Tatkal (Indian Railways, Jun 2025). That's a share of *login attempts*, not of tickets or failed bookings.
- **31,814 tickets in one minute** on 22 May 2025, a system-wide record.
- The next-generation reservation system targets **1.5 lakh+ bookings a minute**, up from 32,000.

These numbers show load. They don't tell you which user failure to fix first.

## 3. Credit where due

| Area | What's live | Since |
| --- | --- | --- |
| Fairness | Aadhaar OTP for Tatkal; agents blocked for the first 30 minutes | Jul 2025 |
| Bots | CAPTCHA, anti-bot and CDN controls; 3 crore+ suspicious IDs deactivated | 2025 |
| Speed | IRCTC eWallet and saved passenger (Master) lists | Already live |
| Capacity | Next-generation reservation system | Target, 2026 |

The gap isn't missing features. It's what happens between 10:00:00 and your PNR.

## 4. Diagnose first: one miss, three causes

| Cause | What happened | The right fix |
| --- | --- | --- |
| **System failure** | Login, availability or payment broke while seats were still available | Reliability: fix the bottleneck and payment recovery |
| **Quota gone** | Seats sold out before your turn; more servers can't add berths | Honesty: say so clearly and offer opt-in alternatives |
| **Status unclear** | Charged? PNR pending? Doubt makes every miss feel broken | Clarity: live status and automatic refunds |

**Step 1 of any fix:** record one outcome for every attempt (PNR / system failure / quota gone / payment pending), and measure errors and p95 latency at each step. Don't roll everything into one "booking failed" rate.

## 5. My fix: queue first, then hold the seat

| When | Step | What happens |
| --- | --- | --- |
| From 9:45 AM | **1. Join a waiting room** | Log in with Aadhaar OTP. At 10:00 you get a queue position and an ETA. The system admits people only as fast as it can book, so there's no refresh war. |
| While you wait | **2. Use the wait** | Confirm passengers from your saved list, pick a backup train, top up your IRCTC wallet. A live view shows your place and seats left. Your turn becomes one tap. |
| Your turn | **3. The berth is held** | Pick train and class; the berth is held for you with a visible timer. The hold length is set per payment method from real completion data, so eWallet gets a shorter hold than UPI or cards. |
| Payment | **4. Pay, or pass it on** | Success: PNR straight away. Failure or timeout: the berth goes to the next person in the queue, and your refund starts automatically. |

Nobody fights for a seat they can't pay for. Nobody loses one to a slow gateway.

## 6. Trade-offs I'd own

| The problem my fix creates | My call |
| --- | --- |
| Holds can lock up seats | One active hold per verified user; short, method-based timers; unpaid holds return to the queue instantly |
| Bots will camp the queue | Only Aadhaar-OTP verified users get a queue slot, one slot per user per journey date |
| A queue doesn't add seats | Show seats left vs people ahead, so users can switch to a backup train early. No auto-switching without consent |
| Debit without a PNR | Reconcile payment before releasing a berth. Never re-sell a seat that may already be paid for |

## 7. How I'd know it worked

**Illustrative pilot targets:**

- **↓ 50%** misses from system failure while quota was available
- **0** unresolved debits without a PNR
- **< 3 min** p95 time from your turn to a clear outcome

**Pilot:** baseline → limited pilot on matched busy routes and peak windows → review → expand only if the targets hold. **Stop on any payment or inventory mismatch.** Keep sold-out outcomes separate, so a busy day isn't mistaken for a system failure.

## 8. What this taught me

1. **Credit what's shipped before proposing anything.** eWallet and saved passenger lists already solve checkout speed.
2. **Separate the causes before choosing the fix.** A queue changes the order; it can't fix an outage or add seats.
3. **Every fix creates a new problem.** The seat hold is only good if holds can't be hoarded and payments always reconcile.

---

## Sources

- Ministry of Railways / PIB, Jun 2025: bot share of early logins, booking record, Tatkal rules
- PIB, Feb 2026: suspicious user IDs deactivated
- PIB Research, 2026: next-generation reservation system target
- [MediaNama, Jun 2025: bot share of early logins, anti-bot system](https://www.medianama.com/2025/06/223-indian-railways-tackles-tatkal-booking-problems-with-anti-bot-system/)
- [Business Standard, Oct 2025: Diwali Tatkal outage and user posts](https://www.business-standard.com/india-news/diwali-rush-irctc-website-crashes-before-tatkal-bookings-users-frustrated-125101700604_1.html)
- [Business Today, Jul 2026: eWallet and Master List](https://www.businesstoday.in/latest/trends/photo/2-new-irctc-features-and-3-secret-tricks-that-make-tatkal-booking-10x-faster-544575-2026-07-22)
