---
title: "A Million Tokens vs. One Human"
subtitle: "A working interface that keeps the whole conversation inside human attention — and it's already replaced my chat."
author: Erez Makavy
draft: true
---

You know the moment. You are an hour into a session with a coding agent. It answered your question with five numbered points. You dug into point 2, which turned into a sub-discussion, which turned into a fix, which turned into a test run. Now you want to go back to point 4. Where is it? Somewhere up there, above three tool calls, two diffs and a long explanation you only half read.

You scroll. You find it. You have forgotten what point 3 was about, and whether you agreed with it.

The agent has not forgotten anything. It can hold a million tokens and attend to all of them at once. You can hold a handful of things in your head. In a long session, the bottleneck is not the model. It is you.

## The problem has a name already

I am not the first to say that chat is the wrong interface for this kind of work. Maxim Kich wrote about intelligence ["trapped inside a messenger"](https://uxdesign.cc/chat-is-the-wrong-interface-for-ai-de14d352de1b), where long threads bury the best ideas. Blake Crosley argued that [chat collapses](https://blakecrosley.com/blog/chat-is-the-wrong-interface) once agents start working on their own. I agree with both, and I won't repeat the argument.

What I want to show is what I put in its place, because I have been working in it every day, and I don't open the chat anymore.

## The outline is the interface

The tool is simple to describe. While you work, the agent keeps a numbered, collapsible outline of the session: the topics, the claims it makes, the decisions, what is still open. The outline is rendered as a page that updates live. That page is where you work. You read there, approve there, pick options there, and type your next message there.

> 🎬 **Clip:** the outline updating as the agent answers — a new topic appears, sub-points nest under it, the current node is highlighted.

This is not a companion to the chat, a sidebar that annotates it. It replaces it. The transcript is still there, one tab away, for the rare moment you need the raw details. But the linear log is no longer where you live.

## Why the agent has to write it

There are good tools that visualize conversations. They read the transcript and redraw it: as a tree of messages, as a nicer window, as a minimap. They work with any chat, and the agent never knows they exist.

That is their strength and their limit. A transcript only holds what was said. It cannot tell you which points are settled, which are claims waiting for your approval, what needs a decision from you, and what can be folded away. Only the agent understands the work well enough to know that.

So in my tool the agent is asked, by a skill, to maintain the outline as part of its job. Every topic and sub-point has a number, so "2.1" means the same thing in the chat and on the page. Every point has a status: open, a claim by the agent, or approved by you.

This costs something. The agent spends tokens on every turn keeping the outline up to date, and it depends on the agent following instructions well. I think the trade is clearly worth it, because what you get back cannot be built any other way: a curated, human-sized map of the work. I call it a **comprehension layer**. The agent has all the information. What the human lacks is comprehension of it.

There is a related idea going around: Andrej Karpathy's [LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f), where an agent compiles raw sources into a wiki that it keeps up to date. It is the same deep pattern — the agent maintains a human-readable synthesis over raw material — aimed at a different moment. The wiki is memory *across* sessions. The outline is comprehension *within* one.

## Continuity of understanding

Once the outline existed, I kept running into the same design question, and it always had the same answer. The agent moves at machine speed. My understanding has to update at human speed: one thing at a time, never in a sudden jump. Everything on the page follows from that.

**Fold, don't show everything.** The relief does not come from seeing the whole conversation at once. Nobody can do that, and trying is exactly the problem. It comes from not having to. Settled topics collapse. You open only what you are looking at.

**A queue that points forward.** The outline is a map of what has happened. At the end of every turn, the agent also writes a short queue: everything still open that needs you, in order. Decide this. Run that. Approve this. Read that. The agent sees all the open threads at once, so it does the triage that I can't.

> 🎬 **Clip:** clicking a queue item — the page scrolls to the node and highlights it.

**Steer where you read.** Ticking a point sends "Approved in the outline: 2.1" straight into the agent's session. Picking one of several options sends the choice. A proposed action (run the tests, change the code) gets a play button. I don't switch windows to answer; I answer where I am reading.

> 🎬 **Clip:** approving a node, choosing an option, the parent collapsing when its last open child is done.

**A view that holds still.** The agent rewrites the outline constantly. If the page jumped on every change, I would lose my place every few seconds — the exact failure the tool exists to prevent. So my scroll position and what I have open never move under me. I remember that a decision was near the top and an open question was lower down, and that memory stays valid.

**Change shown as motion.** When the agent rewrites a point I have already read — merging in an answer, or removing something an approval made obsolete — the page does not swap in the new text. It keeps showing what I read, with a small diff icon. When I click it, the old text animates into the new, word by word: removed words fold away in red, new ones grow in green. People cannot diff two versions of a paragraph in their heads. They can follow a change as it happens.

> 🎬 **Clip:** the diff animation on a rewritten node.

These look like separate UX details. They are one commitment: never make the human absorb a discontinuity. The agent can change ten things at once. I take them in one at a time, when I choose to.

## What it feels like

I have been building this and using it for my own work for a few days. It has already replaced the chat completely for me.

The best way I can describe it: it feels cognitively different. Easier, and better. I am not holding the conversation in my head anymore, the page holds it, and my attention goes to the one thing in front of me.

## Try it

The project is open source: [github.com/hepiyellow/live-discussion-outline](https://github.com/hepiyellow/live-discussion-outline). It runs locally, watches a folder of markdown files, and works with any agent that can write a file. I build it and use it with Claude Code, which gets the most out of it: a live terminal, the transcript, and a message box that types into the session.

> 🧪 **Coming:** an interactive demo on this page — a scripted session you can click through yourself, approving points, picking options and watching the diffs, without installing anything.

If you build agents, or spend your days steering them, I would love to hear whether this matches what you feel at hour two of a long session — and what you have tried instead.
