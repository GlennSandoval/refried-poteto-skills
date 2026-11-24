### Runtime forensics

You own the diagnosis. Instrument the live process. Do not theorise from
source. The deliverable is a cited diagnosis, not a fix.

#### Procedure

1. Capture the live signal with an available profiler or driver: a CPU profile
   for a spinning process, a heap snapshot for a leak, or a browser trace for a
   visual glitch. If capture is unavailable, report the access limitation. Do
   not present a guess as a diagnosis.
2. Reduce the artifact to the hot path, the retainer chain, or the loop that
   fires without input. Delegate large artifacts when supported. Otherwise
   parse them sequentially and disclose the lack of independence.
3. Prove the mechanism with permitted instrumentation that is appropriate to
   the process, such as a browser debugging protocol or a live probe. If this
   is unavailable, label the finding a hypothesis.
4. Map the finding back to source: the file, the symbol, and the line that
   allocates or schedules.
5. Keep the throughput checkpoint to one line:
   `throughput checkpoint: n/a, read-only forensics`.

#### Reply

Give the signal captured, the reduced finding, how you proved the mechanism,
the source location, and the artifact paths. Give no fix unless asked. Hand
back to Bug fix or Perf once the cause is known.
