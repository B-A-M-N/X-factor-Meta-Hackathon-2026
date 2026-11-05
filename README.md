# X-Factor

**Making AI agents useful when I can't be sitting at the keyboard.**

Meta Global AI Developer Hackathon 2026 · Indie Developer · [John London / B-A-M-N](https://github.com/B-A-M-N)

X-Factor is four independent, open-source infrastructure projects that I'm trying to make work together: **Locus, Ocliv, Metis, and Jeverb**. They're not four different chatbots. Each one deals with a problem I've run into while trying to get AI agents to do actual engineering work.

## Why I built this

I'm 37, a single father raising a six-year-old son, and I've been out of work for a while. I love working on AI infrastructure, but I don't have a team of engineers, an unlimited cloud budget, or eight uninterrupted hours a day to babysit terminals.

My son needs me. Sometimes that means I have to drop what I'm doing and walk away from the computer. And as he gets older, I need to be able to do that *more*, not less.

That's the engineering problem behind X-Factor.

I want to hand an agent a real task, let it work on an actual machine, see what it's doing, and have something better than its word for whether the job got done. I want to use the hardware and providers I can afford. I want to be able to step away without losing the whole thread or trusting a green checkmark that doesn't mean anything.

I've spent a lot of time getting agents to write code. The harder part has been making all the stuff around them reliable: routing inference, connecting machines securely, keeping sessions straight, knowing when work actually ran, and checking the result. That's what I'm building here.

This isn't about replacing my judgment or pretending I've solved autonomous development. I want infrastructure that gives me more control over the work while demanding less constant attention from me.

## The four projects

| Project | What it does | Repository |
| --- | --- | --- |
| **Locus** | A local inference gateway for routing across providers, managing capacity, isolating credentials, and seeing what requests actually did. | [B-A-M-N/Locus](https://github.com/B-A-M-N/Locus) |
| **Ocliv** | Self-hosted tunneling and authenticated HTTPS/MCP access so an external controller can reach services on my machines without exposing them carelessly. | [B-A-M-N/ocliv](https://github.com/B-A-M-N/ocliv) |
| **Metis** | A terminal-based control surface for launching, observing, and interacting with *real* agent sessions, plus an MCP interface for authorized controllers. | [B-A-M-N/metis](https://github.com/B-A-M-N/metis) |
| **Jeverb** | An experimental layer for bounded Jev judgments, policy-controlled workflows, execution receipts, and verification boundaries. | [B-A-M-N/Jeverb](https://github.com/B-A-M-N/Jeverb) |

**This is an umbrella/index repository, not a monorepo.** Each project has its own source, dependencies, documentation, tests, and release process. They are useful separately, and the point of X-Factor is to connect them without turning them into one giant codebase.

## How the pieces fit

The basic idea is simple:

1. **Locus** gives coding agents a shared way to reach configured inference providers, with limits and operational evidence.
2. **Ocliv** provides an authenticated route from an external controller to a service running on my hardware.
3. **Metis** receives authorized instructions, starts or accesses an actual worker session, and lets me observe and steer that session.
4. **Jeverb** explores how bounded decisions, policy, and independent evidence could make agent workflows safer to trust.

The proven controller-to-worker path is:

```text
Authenticated scripted controller
            |
            v
     Ocliv HTTPS / OAuth
            |
            v
         Metis MCP
            |
            v
       Real Muse worker
            |
            v
   Test failure -> code fix -> tests pass
            |
            v
      Recorded test + diff evidence
```

**Locus** is the inference gateway alongside that execution path; it isn't the orchestrator. **Jeverb** is a separate experimental control and evidence project, not a production verifier for the demo run.

The intended longer-term experience is to give a controller like Meta.ai an objective and watch it coordinate real workers through this infrastructure. The distinction between that goal and what I've actually demonstrated matters.

## What I can actually show

In an isolated demonstration, an authenticated controller reached Metis through Ocliv, provisioned a real PTY-backed coding worker, and gave it a deliberately failing Python test to fix. The worker changed the code and reran pytest: **one failing test became three passing tests**. The result is backed by test output and a minimal source diff, not just an agent saying “done.”

I've also observed live Muse inference traffic through Locus, and Ocliv has separately qualified an authenticated MCP path through a public HTTPS relay. Jeverb has deterministic demonstration and test evidence for selected control behaviors.

Those are **specific demonstrated paths**, not proof that all four products are production-ready or that every possible integration is finished.

### What I'm not claiming

- **Direct Meta.ai → Ocliv → Metis orchestration:** not independently proven end to end as of this README update. A scripted controller is not a Meta.ai-originated tool call.
- **Jeverb verifying the integrated coding run:** not demonstrated. Jeverb remains experimental; model reliability and production completion are not generally qualified.
- **General autonomous reliability:** a successful fixture run is evidence for that fixture, not a guarantee for arbitrary repositories or long-running missions.
- **Universal deployment readiness:** self-hosted access, credentials, operating environments, and provider limits still have real constraints.

I would rather tell you where something stops working than make the README sound more finished than the code is.

## How Meta fits in

I used **Meta's Muse models and Muse Code** as hands-on coding tools while building, debugging, testing, and integrating these systems. This wasn't just a brainstorming exercise: the work involved real code, tests, session management, and debugging integration failures.

Locus includes a Meta provider adapter with dedicated routing and stream/error tests, and there is recorded live Muse inference traffic through the gateway. Metis supports real Muse worker sessions. A direct Meta.ai-driven controller workflow remains an integration objective until it can be shown with actual Meta-originated actions and corresponding worker evidence.

## Explore and reproduce

Start with the individual repositories above. Each maintains its own README, setup instructions, tests, and limitations:

- [Locus documentation](https://github.com/B-A-M-N/Locus/tree/feat/security-principal/docs)
- [Ocliv documentation](https://github.com/B-A-M-N/ocliv/tree/master/docs)
- [Metis documentation](https://github.com/B-A-M-N/metis/tree/master/docs)
- [Jeverb documentation](https://github.com/B-A-M-N/Jeverb/tree/main/docs)

The integrated demo uses a separate local harness with a disposable failing-test fixture. It is intentionally isolated from the four product repositories so that demonstrating a repair doesn't mean modifying the products themselves. No public demo-harness source or video link is implied by this index.

Some supporting work predates the October 27–November 4, 2026 hackathon build window. The individual projects' histories and documentation should be used to distinguish earlier work from additions made for the event; this index does not represent all existing code as newly written during the hackathon.

## Where I want this to go

I don't need another agent that tells me everything went great.

I need systems that can do the work, show me what happened, admit what they don't know, and give me enough control to trust the process without staring at it every second.

**I don't want AI to replace my judgment. I want infrastructure that lets me spend less time supervising machines, and more time being a father.**
