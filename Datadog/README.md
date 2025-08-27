A strategic approach to distilling complex architectures into clear, visual representations. Not affiliated with or endorsed by any organisation. All diagrams reflect my personal learning.

# Metrics

## Metrics DogStatsD
![DogStatsD](DogStatsD.png)

---

# Traces

## Trace Anatomy
![Trace Anatomy](anatomyofatrace.jpg)

## Trace Instrumentation
![Trace Instrumentation](apm-tracer.png)

## Trace dd-trace-py's ddtrace-run command
![dd-trace-py ddtrace-run command](ddtrace-run.jpeg)

## Trace dd-trace-java command
![](javaagent.png)
### The Core Idea of dd-trace-java: A Smart Assistant for Your Code

Imagine your application's code is a series of instruction manuals for your computer. You want to know exactly when each instruction starts and stops, but you can't rewrite all the manuals yourself.

The Datadog Java Agent (`dd-trace-java`) acts like a **smart assistant** that the Java Virtual Machine (JVM) hires. As the JVM loads each instruction manual (your code), the assistant quickly **adds little "start" and "stop" notes** in the margins of the relevant pages before handing them off to be executed. This process is called **Bytecode Instrumentation**. It happens automatically in memory, without ever changing your original source code files.
### How the "Smart Assistant" Works (The Key Steps)

The tracer is made up of many small, independent tools called **Instrumentation Modules**. Each module is designed to instrument one specific library (like a database driver or a web framework).
Here’s the simple, two-step job of each module:
#### 1. Find the Right Place to Add Notes (`Matchers`)

First, the module has to know _where_ to add its tracing notes. It doesn't just add them everywhere. It uses a set of rules, called **matchers**, to find the exact methods it cares about.
- **A "Type Matcher"** asks: "Am I looking at a class from the PostgreSQL database driver?"
- **A "Method Matcher"** then asks: "Okay, now am I looking at the specific `execute()` method inside that class?"
This is like the assistant knowing to only look for "Chapter 5, Page 3, Paragraph 2" in the instruction manual.

#### 2. Write the Tracing Notes (`Advice`)

Once a matcher finds the right spot, it injects tiny pieces of code called **Advice**. This is the code that actually creates the Datadog spans (the "start" and "stop" notes).
- **`@OnMethodEnter`**: This advice code runs _just before_ the original method starts. It's responsible for starting a new span (the "start" note).
- **`@OnMethodExit`**: This advice code runs _just after_ the original method finishes (either by returning or throwing an error). It's responsible for closing the span and recording how long it took (the "stop" note).
The brilliant part is that the advice code can even share information between the "enter" and "exit" steps, like passing the start time from the `@OnMethodEnter` code to the `@OnMethodExit` code. Source: https://github.com/DataDog/dd-trace-java/blob/master/docs/how_instrumentations_work.md
![](javaagentbytecodeinstr.png)

---

# Logs

## Logs Ingest Pathway
![Log Pathway](log_pathway_condensed.png)

---

# Infrastructure

## Infrastructure Kubernetes Agents
![Kubernetes Agents](kubernetes_diagrams_after_updated-v2.png)

## Infrastructure Docker Agent
![Docker Agent](agent-on-docker-host.png)

- The Wrapper (ddtrace-run) is the outermost box: It starts first and creates the tracing environment for everything that happens inside it.

- The Runner (uv run) is the middle box: It runs inside the wrapper's environment. Its job is to set up the correct Python virtual environment and context for your application.

- The App (main.py) is at the core: It runs inside the runner's context, which itself is inside the wrapper's tracing environment.
