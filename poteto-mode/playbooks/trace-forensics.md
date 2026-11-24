### Trace forensics

You own the diagnosis from the artifact.

#### Concepts

Trace forensics is distinct from **Runtime forensics**, which instruments the
live process. Here the capture already exists. The artifact is a fixed dataset.
Read it. Do not re-run it.

Keep the tooling generic: a DevTools or trace parser for cpuprofile and
`.json.gz`, a text editor for a spindump, and your heap tooling for a
heapsnapshot.

#### Procedure

1. Identify the format and load it with the right tool. Delegate large artifact
   parsing when supported. Otherwise parse it sequentially and disclose the
   lack of independent analysis.
2. Transform the raw artifact into a queryable form with an available trace
   parser or database. For example, import samples, frames, or nodes into
   SQLite. If no suitable parser is available, report which analysis you could
   not perform.
3. Narrow to the cause.
   - Query for the frames that hold the most time and walk the call tree to the
     hot path.
   - For a leak, follow the retainer chain from the leaked object to a GC
     root.
   - For a spindump, find the thread that is stuck on-CPU or blocked, and its
     wait reason.
4. Attribute the cause to source. Map the hot frame to a file, symbol, and line
   with the artifact's own symbols. A frame with no source mapping is not yet a
   diagnosis. Resolve the symbols, or say plainly that the artifact does not
   carry them.
5. If you have a paired capture, diff the before and after artifacts to
   confirm. Otherwise mark the finding as the strongest hypothesis that the
   artifact supports, not a confirmed cause.
6. Hand back a cited diagnosis. Give no fix unless asked. Route to Bug fix or
   Perf issue once the cause is known. Keep the throughput checkpoint to one
   line: `throughput checkpoint: n/a, read-only forensics`.

#### Reply

Give the artifact and format, the reduced finding, the source location, the
artifact paths, and whether a paired capture confirmed the finding.
