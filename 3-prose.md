# Prose

<a id="p.documentation"></a>

**[P.documentation](#p.documentation). Keep comments and documentation accurate to the current system.**

*Requirement. [Coherence](PRINCIPLES.md#coherence), [Verification](PRINCIPLES.md#verification)*

Put accounts of what changed and why in change records.

Readers should be able to rely on descriptions of the system without knowing an earlier implementation. Describe current behavior, constraints, and lasting reasons. Put accounts of what changed and why in change records. Placement and duplication follow the [documentation conventions](#c.documentation.locations).

## General writing

As general writing guidance, write for readers who do not share your context. Explain what the surrounding artifact cannot readily show. The rules below make sentence structure, terminology, and punctuation easier to follow.

<a id="c.prose"></a>

**[C.prose](#c.prose). Prose clarity**

*Editorial preference. Policies [P.documentation](#p.documentation), [P.commit-explanations](4-history.md#p.commit-explanations), [P.pr-explanations](modules/pr.md#p.pr-explanations).*

Apply these conventions to prose sentences.

**Sentence structure**

- <a id="c.prose.focus"></a>**[C.prose.focus](#c.prose.focus). Keep one main idea per sentence.** Split sentences that make separate claims readers need to assess independently.

- <a id="c.prose.flow"></a>**[C.prose.flow](#c.prose.flow). Order information from familiar context to new information.** Readers should be able to follow the sentence from left to right.

- <a id="c.prose.subject-verbs"></a>**[C.prose.subject-verbs](#c.prose.subject-verbs). Keep subjects close to their verbs.**

**Actors and references**

- <a id="c.prose.actors"></a>**[C.prose.actors](#c.prose.actors). Make clear who or what performs each action.** Name the actor when the sentence would otherwise leave it unclear. Assign actions to the entities that actually perform them.

- <a id="c.prose.pronouns"></a>**[C.prose.pronouns](#c.prose.pronouns). Use pronouns only when their referents are clear.** Repeat a name when a pronoun could refer to more than one entity.

- <a id="c.prose.explicit-nouns"></a>**[C.prose.explicit-nouns](#c.prose.explicit-nouns). State what is being described or compared.** Include the noun when readers would otherwise have to guess what has the stated property.

- <a id="c.prose.modifiers"></a>**[C.prose.modifiers](#c.prose.modifiers). Place descriptive phrases next to the words they describe.** Rewrite a phrase when readers could connect it to the wrong person or thing.

**Word choice**

- <a id="c.prose.terms"></a>**[C.prose.terms](#c.prose.terms). Build explanations from common words and from concrete names in the material.** Avoid technical jargon. When a technical term is necessary, define it in plain words before relying on it. For established project terms, link an existing definition when needed.

- <a id="c.prose.hyphenation"></a>**[C.prose.hyphenation](#c.prose.hyphenation). Avoid invented hyphenated compounds.** State the action or relationship in an ordinary phrase. For example, prefer "selects the first successful alternative" to "first-success selection". Established compounds and standard prefixes are acceptable when they read naturally. Preserve hyphens in identifiers, URLs, proper names, and exact quotations.

- <a id="c.prose.literal-language"></a>**[C.prose.literal-language](#c.prose.literal-language). Prefer literal descriptions to metaphors.** Use the actual operation, constraint, or relationship when a metaphor would leave readers to infer the meaning.

**Punctuation**

These punctuation choices support [one main idea per sentence](#c.prose.focus) and [the progression from familiar to new information](#c.prose.flow).

- <a id="c.prose.punctuation"></a>**[C.prose.punctuation](#c.prose.punctuation). Replace semicolons, em dashes, and colons that join statements with clearer punctuation or separate sentences.** Use periods, commas, or parentheses according to the relationship being expressed. A colon may introduce a list. Preserve punctuation required by code, URLs, message syntax, source references, and exact quotations.

- <a id="c.prose.parentheses"></a>**[C.prose.parentheses](#c.prose.parentheses). Prefer parentheses only for brief qualifications.** Put a separate claim or an essential step in the explanation in its own sentence.

## Comments

<a id="c.comments.purpose"></a>**[C.comments.purpose](#c.comments.purpose). Use comments for constraints and reasons absent from the code.**

*Default. Principle [Coherence](PRINCIPLES.md#coherence). Policy [P.documentation](#p.documentation).*

Names, types, and implementation often supply the explanation. Add a comment when a constraint or reason is not evident from them. Accounts of what changed and why belong in change records under [P.documentation](#p.documentation).

Before adding a comment, consider whether a clearer name, smaller function, or stronger type can express the information. Omit comments that only paraphrase code, repeat a name, or label the next block.

A reader should be able to understand a comment without seeing an earlier version of the code.

<a id="c.comments"></a>

**[C.comments](#c.comments). Comment placement and idiom**

*Default. Policy [P.documentation](#p.documentation).*

- <a id="c.comments.definitions"></a>**[C.comments.definitions](#c.comments.definitions). Use function definition comments for caller-visible facts not evident from the signature.** For example, explain a required input order here.

- <a id="c.comments.bodies"></a>**[C.comments.bodies](#c.comments.bodies). Use function body comments for non-obvious constraints or choices.** These can explain invariants, external constraints, specification rules, or implementation choices.

- <a id="c.comments.idiom"></a>**[C.comments.idiom](#c.comments.idiom). Match the surrounding code's comment style and density.**

- <a id="c.comments.placement"></a>**[C.comments.placement](#c.comments.placement). Place comments beside the code they explain.** Refer to identifiers visible at that location so readers can connect the explanation to the code.

- <a id="c.comments.callers"></a>**[C.comments.callers](#c.comments.callers). Put caller-specific explanations at the caller.** A condition specific to one use belongs beside that use. A condition all callers must satisfy belongs in the function's contract.

- <a id="c.comments.interfaces"></a>**[C.comments.interfaces](#c.comments.interfaces). Put caller-facing explanations in interface documentation when a separate interface exists.** Readers should find the contract where they look up the operation.

- <a id="c.comments.brevity"></a>**[C.comments.brevity](#c.comments.brevity). Prefer brief comments.** As guidance, one sentence often suffices. If a comment needs several sentences, consider whether clearer names, a smaller function, or a stronger type could express some of the information. Keep the explanation when the code cannot express it.

## Documentation

<a id="c.documentation.locations"></a>**[C.documentation.locations](#c.documentation.locations). Give each explanation an authoritative home by default.**

*Default. Principle [Coherence](PRINCIPLES.md#coherence). Policy [P.documentation](#p.documentation).*

Link to the explanation instead of maintaining competing copies. Put setup and usage guidance in the relevant README, and keep component-specific details near the component.

Comments and documentation describe the current system under [P.documentation](#p.documentation).

### Markdown presentation

<a id="c.markdown-wrapping"></a>

**[C.markdown-wrapping](#c.markdown-wrapping). Do not hard-wrap Markdown paragraphs or bullet text.**

*Editorial preference. Principles [Coherence](PRINCIPLES.md#coherence), [Proportionality](PRINCIPLES.md#proportionality).*

Keep each paragraph or bullet's text on one source line and let the renderer wrap it. Preserve line breaks required by code blocks, tables, or other Markdown structure. This also applies to PR bodies.

<a id="build-and-checks"></a>

### Build and checking documentation

<a id="c.checking-instructions"></a>**[C.checking-instructions](#c.checking-instructions). Keep build and checking instructions with the component they apply to.**

*Default. Policy [P.documentation](#p.documentation).*

Document formatter versions, commands, and prerequisites in the relevant component guide. Link those instructions instead of maintaining another command list here. The [workflow guide](modules/spectec.md#spectec-build-and-checks) provides compiler command recipes.
