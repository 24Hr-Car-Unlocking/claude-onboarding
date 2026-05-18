# What "vibe coding" actually means

<br>

> Vibe coding is **not** prompting and hoping.
>
> Vibe coding done right = **you are the architect and reviewer; Claude is the implementer.**

<br>

Output quality depends entirely on the **protocol** you follow — not on how clever your prompts are.

Note:
Most people who fail at vibe coding fail because they treat Claude like a magic genie. They give vague prompts, accept vague output, and ship vague software. The fix isn't a better LLM. The fix is a better process.

---

## The two failure modes

### ❌ Slop mode

"Make me a feature that does X" → you copy-paste whatever comes out → it half-works → you ship it → bugs in production → you have no idea why.

### ❌ Helicopter mode

You micromanage every line of code → you might as well have written it yourself → no leverage, no speed, no point.

---

## The shape of _legitimate_ vibe coding

```
1. You write (or co-write) a SPEC describing what to build
2. Claude reads the spec + repo, drafts a PLAN
3. You review the plan, push back, refine
4. Claude implements TEST-FIRST, in small atomic steps
5. You review the diff at the end of each step
6. Conventional commits → PR → squash merge → deploy
```

This is the same loop senior engineers use. The only difference is _who types the code_.

---

## The non-negotiables

You will never let Claude:

- Write code without a spec
- Commit without your approval
- Push without your approval
- Mark work "complete" before it's actually deployed
- Skip writing tests
- Skip writing a PR description

Everything else in this deck exists to make those rules easy to follow.

Note:
If you remember nothing else from this presentation, remember this slide. These six rules are the entire game.
