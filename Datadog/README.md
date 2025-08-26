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
