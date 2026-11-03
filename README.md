# prompt-enhance

An agent skill that rewrites a rough request into a sharper prompt, then runs it.

Most prompt enhancers make requests *look* more specific by filling gaps with guesses: a line number, a framework, an output format nobody asked for. This one is built around avoiding that:

- **Only checked facts.** Anything stated as fact in the enhanced prompt must come from the user's request or from something the agent checked that turn. Everything else becomes a "check this first" step or an explicit `(assumption)`.
- **Risk-based checkpoint.** Read-only requests (lookups, explanations, analysis) are shown and run in the same turn. Write actions, assumptions, or requests with more than one reasonable reading wait for confirmation. No more doubled round trips for simple questions.
- **Pass-through.** Approval replies like "go ahead" or "next" are never enhanced, and requests that are already clear run as is.
- **Tuned for Claude Opus 5.5.** No "think step by step" boilerplate, vague quality words turned into concrete criteria, pasted text kept apart from instructions. Based on [Prompting Claude Opus 5.5](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-opus-5-5).

Works in English and Korean. Replies follow the language of the request.

## Install

```bash
npx skills add Hoya-kim/prompt-enhance
```

Or copy `skills/prompt-enhance/` into your agent's skills directory (for Claude Code: `~/.claude/skills/`).

## Usage

```
/prompt-enhance hmm, why is this doing that?
```

Example of a blocking checkpoint, for a write action:

```
━━━━ Prompt Enhanced ━━━━
📝 Original:
clean up this component a bit

✨ Enhanced:
[Task] Refactor UserCard.tsx: split the 180-line render into subcomponents. Keep props and behavior unchanged.
[Done when] Existing tests pass.

📌 Changes:
- Resolved "this component" to UserCard.tsx (checked: open file)
- Scope limited to splitting render, no behavior change (assumption)

Run this? (y / edits / n)
━━━━━━━━━━━━━━━━━━━━━━━━
```

## Files

| File | Purpose |
|------|---------|
| `skills/prompt-enhance/SKILL.md` | The skill itself |
| `skills/prompt-enhance/GOTCHAS.md` | Failure modes the rules are built to prevent |
| `skills/prompt-enhance/evals/cases.md` | Manual test cases with expected behavior and fail signals |

## 한국어

거친 요청을 더 나은 프롬프트로 다듬은 뒤 실행하는 에이전트 스킬입니다.

- **확인한 사실만 넣습니다.** 강화본에 사실로 쓰는 내용은 사용자 발화에 있었거나 그 턴에 직접 확인한 것이어야 합니다. 나머지는 "먼저 확인할 것" 단계나 `(가정)`으로 표시합니다.
- **위험도에 따라 확인합니다.** 조회·설명·분석은 강화본을 보여주고 바로 실행합니다. 쓰기 작업, 가정이 있는 경우, 해석이 갈리는 경우에만 확인을 기다립니다.
- **승인 응답은 건너뜁니다.** "진행해", "응", "다음"은 강화하지 않고, 이미 명확한 요청은 그대로 실행합니다.

트리거: `/prompt-enhance`, "프롬프트 강화", "이거 다듬어서 실행해", "질문 다듬어줘", "요청 강화해줘"

## License

MIT
