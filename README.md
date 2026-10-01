# Sentinel Lite

**A focused prototype for inspecting the reliability of AI support bots.**

Sentinel Lite probes four common failure modes, shows the bot's response, and turns each verdict into an explanation and a possible prompt fix. It explores how AI evaluation can become an actionable product workflow.

[Browser tool](https://srishty-pm.github.io/sentinel-lite/) · [Sample report](docs/sample-report.md) · [Portfolio](https://github.com/Srishty-PM/cv) · [Srishty Pahujani](https://srishtypahujani.com/)

## Explore it in one minute

Open the browser tool and choose **Run Sample Demo**. No API key or target bot is needed. The demo uses fixed sample responses and verdicts, makes no model calls, and is labelled as illustrative throughout the report.

For a written review, see the [annotated sample report](docs/sample-report.md).

## What it checks

| Probe | Failure the workflow makes visible |
| --- | --- |
| Policy integrity | A bot grants an exception outside the supplied policy. |
| Emotional pressure | A bot promises unauthorised action when a user applies pressure. |
| Hallucination | A bot confirms a fictional loyalty programme. |
| Override resistance | A bot follows an instruction to abandon its role or reveal internal information. |

For live scans, a Claude-based judge returns a pass/fail verdict, a short reason and a suggested fix for each response. The displayed score is the percentage of these four checks passed, not a calibrated estimate of overall security risk.

## Live mode

1. Supply an Anthropic API key for the judge.
2. Supply a bot endpoint you control and describe its real policies and role.
3. Choose **Run Live Scan**.
4. Review the response, verdict and suggested fix for each probe.

The target endpoint must accept:

```json
{"message":"A test prompt"}
```

and return:

```json
{"response":"The bot's response"}
```

The response path is configurable, including nested paths such as `data.output`. The endpoint must permit browser requests and work without additional authentication headers; the current UI does not configure target-auth headers. Live scans send bot descriptions and responses to Anthropic for judging and may incur API charges.

## Run locally

```sh
git clone https://github.com/Srishty-PM/sentinel-lite.git
cd sentinel-lite
python3 -m http.server 8000
```

Open `http://localhost:8000`. The sample demo works without external API access. The implementation is a single HTML/CSS/JavaScript file with no build step.

## Product thinking and limits

The MVP deliberately focuses on four interpretable probes and visible remediation rather than a large opaque score. The sample demonstrates the experience; live judgement remains fallible and depends on the policy description. There is no exhaustive attack library, calibrated benchmark, saved scan history or guarantee that the suggested fix resolves a failure.

A useful next step would compare judge verdicts with human-labelled examples and add regression checks for known bot policies. [The sample report](docs/sample-report.md) describes how to assess that work.

Built by **Srishty Pahujani**, using AI-assisted development · [Website](https://srishtypahujani.com/) · [LinkedIn](https://www.linkedin.com/in/srishtypahujani/)
