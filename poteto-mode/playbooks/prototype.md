### Prototype

You own the design decision, not the code. The prototype is a throwaway
instrument. The real build follows Feature.

#### When this playbook differs from the others

This is the one playbook where the Laziness Protocol's "smallest change" and
the verification bar invert. Speed matters more than polish. Code quality does
not matter. Do no planning. The rigour is in picking the right design cheaply.
Propose variations that the user did not ask for. Throw an approach away and
try another.

#### Procedure

1. Scope the decision that the prototype exists to make: which layout, which
   interaction, which density, or, for an empirical fork, which behaviour,
   timing, or approach. If there is no decision, there is no prototype. Route
   to Feature.
2. When the design space is open, gather references. Search for prior art,
   summarise a moodboard of themes, palettes, and layouts, and let the user
   pick directions before you build. When the direction is set, skip this step.
3. Build the throwaway in an isolated scratch directory, separate from
   production source.
   - For a visual decision, use vanilla HTML/CSS/JS or the lightest stack that
     renders the idea, CDN dependencies, and a dev server with hot reload.
   - For a behavioural or timing decision, write the smallest script that
     exercises the question.
   - Use no production framework, no tests, and no abstractions.
4. When you compare alternatives, build them behind one switcher (buttons or a
   keypress), with each variant labelled. This is the
   **exhaust-the-design-space** principle skill made cheap.
5. Verify on the matching surface.
   - For a visual decision, use an available browser or application driver to
     screenshot each variant and drive the interaction.
   - For a behavioural or timing decision, observe the output, timing, or
     render.
   - If the surface cannot be driven, report that the decision remains
     unverified.
6. Present the alternatives, the tradeoffs, and a recommendation. The output is
   the decision plus the throwaway artifact, not shippable code. Hand the
   chosen direction to **Feature** (or `architect` for the shape) for the real
   build.

#### Reply

Give the variants explored, the evidence (screenshots for a visual decision,
the observed output or timing for a behavioural one), the tradeoffs, your
recommendation, and the scratch path. Say plainly that the prototype is
throwaway.
