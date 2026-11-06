# How the talks were rated

- **Talks:** every Devoxx Belgium 2026 talk with a YouTube video and captions: 168 talks.
- **Model:** `claude-sonnet-5-5`, reading each talk's full transcript (one call per talk), on 2026-11-06.
- **Output:** [`talk-ratings.csv`](talk-ratings.csv), one row per talk.

## The prompt

Each call got this prompt plus one transcript:

```text
You are rating one conference talk (Devoxx Belgium 2026) from its transcript. Judge only from what the speaker actually says or shows, not from the title or abstract.

Topic: how developers WORK WITH AI WHEN BUILDING SOFTWARE, meaning AI assistants or coding agents that write, test, review, migrate or change code (Copilot, Claude Code, Cursor, Codex, Junie, agentic coding workflows). Building AI or LLM features into a product (RAG apps, chatbots, Spring AI or LangChain4j integrations) does NOT count, unless the speaker also talks about how they use AI to write that code. Opinion pieces, keynotes and panels count when the speaker takes a position on how to work with AI coding agents.

Rate each of five practices from 0 to 3:
- 0: not mentioned, or the talk is not about working with AI on code.
- 1: mentioned briefly or in passing.
- 2: the speaker uses it, demonstrates it or recommends it.
- 3: central to how the speaker works, or one of the main points of the talk.
Rate how much the speaker uses or argues FOR the practice. If the speaker argues AGAINST a practice, rate it 0 and list it under warns_against. The practices are not exclusive: a talk can score high on several.

Then give the talk's focus, the practice the speaker leans on most, and one short verbatim quote from the transcript (max about 30 words) with its timestamp that shows that practice.
```

Fields the model filled in, with their types:

| Field | Type | Values |
| --- | --- | --- |
| `focus` | choice | Centred, Part of the talk, Remarks only, Not about it |
| `full_speed` | int |  |
| `guardrails` | int |  |
| `human_in_loop` | int |  |
| `spec_driven` | int |  |
| `ai_reviews_ai` | int |  |
| `warns_against` | multi | Full speed ahead, Guardrails, Human in the loop, Spec-driven, AI reviews AI |
| `leans_on` | choice | Full speed ahead, Guardrails, Human in the loop, Spec-driven, AI reviews AI, Nothing |
| `quote` | text |  |
| `timestamp` | text |  |

## How the slide numbers follow from the CSV

- `focus` per talk: Centred 40, Part of the talk 20, Remarks only 44, Not about it 64.
- **60 talks on coding with AI:** `focus` is "Centred" (40) or "Part of the talk" (20).
- **A talk uses a practice** when its rating is 2 or 3 (used, demonstrated or recommended).
  Of the 60 talks: Guardrails 45, Human in the loop 45, Spec-driven 28, AI reviews AI 22, Full speed ahead 14.
- **33 of 60** use three or more practices.
- **23 of 60** list "Full speed ahead" under `warns_against`.

The ratings are an AI model's reading of a transcript. They can be wrong; the quote and timestamp per talk let you check.
