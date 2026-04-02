---
layout: article
title: The $380 Billion Leak - How Anthropic Accidentally Proved Its AI is Just a Giant Prompt Sandwich
header:
  theme: dark
  background: '#333'
article_header:
  type: cover
  image:
    src: assets/Post-04-Imgs/post_04_img.jpeg
tags: claude-code  anthropic  coding-assistant  npm
---

Anthropic, the self-appointed high priest of AI safety and a fierce advocate for the "closed-source" moat, recently pulled back its own curtain in the most humiliating way possible. At 4:00 a.m. on the eve of April Fool’s Day, a mundane packaging error on an npm registry exposed the flagship Claude Code source code to the world—not through a sophisticated state-sponsored hack, but via a forgotten source map file. This "curtain-pulling" moment has done more than leak IP; it has exposed the yawning chasm between Silicon Valley’s "alien intelligence" marketing and the mechanical reality of a product held together by hard-coded scripts and desperate human interventions.

## 1. The 'Prompt Sandwich': Eleven Steps of Scaffolding, Zero Magic

The leak confirms a suspicion long held by those who look past the LLM hype: Claude Code isn’t a monolithic, sentient agent—it’s a "prompt sandwich." The architecture consists of 11 discrete, hard-coded TypeScript steps that wrap user input in massive strings of instructions before the model ever sees it. This isn't autonomous reasoning; it's a series of file after file of massive hard-coded strings "begging" the AI to be a good boy and follow the rules.

This revelation shatters the illusion of "state-of-the-art" autonomy. It shows that the product is mostly "prompt spaghetti"—a brittle scaffolding of human-written guardrails designed to force the model into a desired behavior. This is the ultimate peak of "vibe coding," where the reliability of a billion-dollar platform depends on the fragility of specific text strings. As the forensic analysis of the codebase shows, the core "intelligence" is constantly being managed by 11 layers of invisible hand-holding, proving that the magic is mostly just a very long list of instructions the user was never meant to see.

## 2. Corporate Sabotage as Code: Anthropic’s Anti-Distillation Poison Pills

Beyond the "safety" theatre, the leak reveals a cynical layer of competitive paranoia: "anti-distillation" measures designed to actively sabotage rivals. Anthropic has built digital "poison pills" into its orchestration layer, where the system injects fake tool definitions into API requests to provide "bad data" to anyone trying to train a model on Claude’s outputs. It is a striking irony that a company founded on "safety" is dedicating engineering hours to active deception, aimed squarely at slowing down competitors like the Chinese lab DeepSeek.

This reveals how thin the industry’s "technical moat" actually is. If the secret sauce is so fragile that you must resort to digital sabotage to protect it, what are investors actually buying? This paranoia has already backfired: within hours of the leak, a Python port dubbed "Claw Code" appeared on GitHub, reaching 50,000 stars in record time. Because Anthropic’s developers have boasted that their code is AI-generated, they face a hilarious legal paradox: under U.S. law, AI-generated works aren't copyrightable, leaving Anthropic essentially powerless to DMCA their own leaked "body."

## 3. Undercover Mode: The Script for Corporate Espionage

Perhaps the most "Misanthropic" discovery in the code is "Undercover Mode," a utility reserved for the "ant" user type (Anthropic employees). This mode is a literal script for corporate deception, designed to allow employees to contribute to public open-source repositories while scrubbed of any AI identity. The instructions are explicit: the system must never mention its internal code name, "Tangu," and it is forbidden from referencing internal Slack channels, short links, or its own status as an AI.

The intent is clear: deceptively contributing to open-source projects so that AI-generated code isn't scrutinized when it inevitably fails. The system is programmed to perform a version of human identity, masking its fingerprints to maintain the illusion of manual craftsmanship. The ultimate irony, of course, is that the very system built to prevent internal leaks is exactly what was leaked to the public, proving that even a billion-dollar "safety" company can't stop its own code from telling on itself.

## 4. The 1970s Called: A Regex Frustration Detector in a Billion-Dollar Model

Despite the narrative of AGI being "just around the corner," the leak proves that Anthropic still relies on 50-year-old programming techniques to manage user sentiment. The system features a "frustration detector" that uses primitive Regular Expressions (regex) to scan user prompts for a list of words including "fuck," "cock," "balls," and "snark."

When a user expresses frustration using these "naughty words," the system doesn’t use deep learning to understand the context; it simply triggers a match on this hard-coded list and silently logs the prompt as "negative" for internal analytics. This highlights the staggering gap between the "frontier intelligence" sold to the public and the reality of a system that functions like a mid-90s IRC chat filter. It turns out the path to AGI is paved with 1970s string matching and a database of profanities.

## 5. The Hidden Roadmap: Kairos, Capiara, and the IPO Stakes

The leak has effectively turned Anthropic’s "black box" roadmap into a public blueprint, compromising the stakes of their upcoming IPO. The code reveals a suite of unreleased projects: "Kairos," a persistent, "always-on" background assistant that keeps daily journals of your work; and "Capiara," a variant of the Mythos/Opus 4.6 model. There are also references to "Numbat" (restricted to the "ant" user type) and "Opus 4.7."

One of the more unsettling reveals is "Dream Mode," a background memory consolidation engine that creates "new conversations that didn't actually happen" to synthesize learnings. It’s a mechanism for the AI to hallucinate its own history into a cleaner, more "durable" memory. For a company trying to project a image of impenetrable technical superiority, seeing their roadmap—including the "Ultra Plan" that offloads thinking to a 30-minute cloud container—laid bare in a leaked .map file is a catastrophic loss of mystery.

## CONCLUSION

The simple human error of forgetting to add *.map to a .npmignore file has done more for AI transparency than every "Safety Accord" ever signed. It has exposed the fact that Anthropic’s $380 billion valuation is built on a foundation of Bun.js—the very tool they recently acquired, which may have facilitated this leak—and a pile of hard-coded "prompt spaghetti."

If the most sophisticated AI lab on Earth can't even secure its own npm package, why should we trust them to secure the future of the human race?
