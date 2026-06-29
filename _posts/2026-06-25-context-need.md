---
title: 'Context Is All You Give'
date: 2026-06-25 12:00:00 -0500
categories: [LLM]
tags: [llm, context-engineering, knowledge-base, mcp, agents]
description: Our part to get more from it
---

LLMs broke into my life, probably like they did for everyone. I can't remember the last task I did without one in the loop. An ad-hoc analysis, sketching out code, a large-scope research project, everyday things like personal-development planning, recurring chores like following the news or routine reporting, even this blog you're reading. LLMs slot instantly into my workflow and double, triple, sometimes 10x my efficiency.

These models took a monumental effort to build. To make one that can do almost everything, the labs had to stack attention and feedforward layers deep enough to link the context and store the knowledge. Let alone all the labeling and human and AI response collection behind the post-training that turns a model from merely predicting the next token into something actually helpful. To me, it's like the Manhattan Project of our age!

Luckily, the smartest minds have handled all of that for us. Using these models can be as simple as a casual conversation. Still, it takes effort to use them well, and "context is all we need" is what I keep feeling after leaning on them across every aspect of my life. Provide the proper context in the right form, and you get the best assistant you've ever had.

### Grounding, not guessing {#grounding}

Hallucination and random responses are probably the biggest headache you'll run into. When the model is unsure about something, it won't stop and fail like a calculator throwing an error. It fails by guessing instead: even with little real confidence underneath, it hands back a complete, fluent, and often wrong answer. It makes something up rather than stopping.

Over time I've settled into three habits that head most of this off, and they go into almost every project I start. I lean on a growing knowledge base, kept under strict rules for updating and querying, so the model has a ground truth to stand on instead of its own memory. I pull the parts of the work that have to be exact out of its hands and give them to deterministic tools, so quality is guarded by code. And I let it write things down as it goes, a CSV of data here, a markdown note there, so results survive from one step to the next and from one session into another.

### The knowledge base {#kb}

It didn't take long, once LLMs were part of my daily routine, to notice I was repeating myself: the same set of context, fed by hand, to all kinds of projects. Rarely is a new project truly independent of the ones before it. There's almost always shared background, a similar domain, the same preferences, the same hard-won lessons. And even for the rare anomaly that really does stand alone, soon enough another project comes along that shares its context. Accumulating all of it in one knowledge base just makes sense.

Such a knowledge base only helps if it can grow continuously and seamlessly, right alongside the daily work it assists. And the more useful it gets, the bigger it gets: a knowledge base is most valuable when it holds a large set of contexts, which is exactly what would swallow a huge chunk of the context window, and dilute the model's attention, if you loaded it all at once. That tension is where the design matters.

What works for me is a pile of small markdown files that link to each other, not one giant document. Any project or conversation starts with nothing more than a high-level table of contents of the repo. From there, the model follows only the links that matter, pulling in the few well-named files that are right on topic and leaving the rest on disk. That's progressive loading: follow the links that help, skip the ones that aren't relevant to the project at hand.

A big pile of files only stays trustworthy if it grows organically with everyday use and stays easy for the model to navigate. A carefully designed maintenance manual is the bedrock for all of that. Believe me, I used to direct every query and update by hand, and I was quickly overwhelmed by the sheer burden of it. The fix is to write the rules down once, where the model can see them, and let it do the upkeep. Reading is mostly what we just discussed: always enter through the index, search out the relevant links, and ground the answer on the pages you find rather than improvising.

Writing is the more interesting half. The first rule is that any update or new page has to respect the small, well-named file convention, so the base stays navigable as it grows. It also helps to give the model a clear sense of taste about what is worth keeping: the lessons genuinely learned rather than a transcript of the chat, the preferences and decisions that will recur, and above all the moments I disagreed with the model and why. And whenever a new note contradicts something already in the base, the rule is to stop and re-confirm rather than quietly write over it.

One more piece of this that I genuinely enjoy is the health check. Roughly once a week, also depending on how much token budget my plan has left that week (only half joking :)), I walk the whole base with the model and ask it to flag inconsistencies across everything in it. A contradiction it surfaces is usually one of three things: a genuinely new circumstance, a drift in my own preferences, or simply me failing to stick to a long-term value. Each is worth a small log entry, and together they make the health check a surprisingly fun act of reflection, where I get to watch myself change as a person over time.

### Replace the exact steps with tools {#tools}

A knowledge base is the bedrock, but it isn't the only place hallucination can creep in. It shows up just as readily in the doing as in the knowing: the model can start off perfectly and slip somewhere later.

Thoughtful instructions help steer it toward correct execution, but we can do more. Most LLM-integrated workflows mix two kinds of work. Take a small research analysis: pulling the raw dataset is a data fetch that has to be exact, fitting a regression or computing a correlation is a calculation that has to be exact, reshaping the variables into the right form is a transformation that has to be exact. None of those should come from the model's memory. But what the result implies, which hypothesis it supports, what to test next, how to frame the finding, that's the open-ended part, and exactly where I want the model thinking freely.

Especially when the workflow is a reusable piece, it pays to identify the exact steps and consider handing them to a predefined tool that returns a deterministic result, instead of letting the model improvise freely from beginning to end.

For those exact steps, instead of randomness leaking into every detail, a tool pulls it back to a much smaller surface: choosing the right tool and specifying the correct inputs from the context so far. The model is good at that small, bounded decision, far better than it is at carrying a long computation in its head without slipping. Each tool becomes a reliable fixed point in a long chain, a place where the workflow can rest on a known-correct result instead of a guess. And adding a quality check to each tool is not much extra work, so every one of those fixed points can also validate its own output, catching problems at the step where they happen instead of at the very end.

Tools can take a lot of forms. In my case, most of the time they're old packages I've built or short shell scripts, all wrapped in a command-line interface and called from the command line. A CLI gives the most flexibility: it lets the model reuse everything I've already developed behind nothing more than a command.

The other choice I reach for is MCP. It's more restrictive and a bit more work to build, but it's a great fit for collaboration. And collaboration isn't only about different people running different models with different preferences, which in my experience is usually fine. The harder problem is the execution environment. Whether the model is driving a CLI agent like Claude Code or Codex, or a desktop chat app, each comes with a very different setup: different access to databases, different packages installed, a different network. A local MCP server smooths that over. With something like FastMCP, it's easy to stand up one unified execution environment, the same data access and the same network, no matter which client is calling.

And whichever form a tool takes, its result still has to get to the next step.

### Files as the intermediate {#files}

A natural follow-up, once tools are in the picture, is how to return their intermediate results. The straightforward way is to let the model read the output of the function call directly. That works until it doesn't, and the clearest case is a large dataset. I can't think of a single situation where loading a big dataset into context is a good idea: it buries the model's attention and it hurts precision. So instead of reading the result, pass it as a file.

A file isn't just a workaround for size, it's a universal channel. The filesystem is shared not only across the steps of one session, but across different agents, and even across different models. It also smooths over the differences between environments: whether the model is running in a desktop app or a command-line agent, almost all of them can reach a file. The execution environments may vary widely in what databases and packages they expose, but a file on disk is the one thing nearly all of them can touch. It's the same instinct the big multi-agent setups follow: each agent keeps its own private context and hands off through a shared file rather than merging memories. The model's context is private; the file is the public channel everything can read.

Files also outlast the conversation. Context is wiped the moment a session ends, but a file stays, so it becomes the memory that lets me stop in the middle and pick up tomorrow. And because every handoff is written down, I can open it when something looks wrong and replay a later step on the same file without redoing the expensive ones before it. The workflow stops being a black box and becomes a sequence of checkable artifacts.

### Bringing it together {#together}

So that's the shape of it. Start with a knowledge base, so the model has facts to work from instead of its own memory. Pull the parts of a workflow that have to be exact into tools, especially when it's something I'll reuse. And pass results between steps as files, so nothing important has to live in the model's head. Three habits, one idea: give the model the right context instead of hoping it remembers.

None of this is complicated, and that's sort of the point. These few habits, plus the discipline of checking a result rather than trusting it when it really matters, do most of the work for me. They cut down the hallucinations, they keep the model's attention on what actually matters, and they turn a one-off chat into a workflow I can run again next week without babysitting it. The model stops guessing and starts standing on something.

At the end of the day, the model is already a remarkably powerful tool, far beyond anything I could build myself. Providing the right context, in the right way, is the small part that's left to me, and it's the part that decides whether all that power actually shows up in my work. Give it that, and it becomes the best assistant I've ever had. Context, it turns out, really is most of what you need.
