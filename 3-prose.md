# Prose

## Checklist

**Each comment, including docstrings**

First pass:

- Does it state a constraint or reason the code cannot show? [R.comments.purpose](#r.comments.purpose)
- Does it describe the code as it is, without referring to an earlier version? [R.documentation-accuracy](#r.documentation-accuracy)
- Does it sit where its readers will look? That means beside the code it explains, at the caller for a condition specific to that caller, or in the interface for a contract all callers rely on. [R.comments.placement](#r.comments.placement), [R.comments.callers](#r.comments.callers), [R.comments.interfaces](#r.comments.interfaces)
- Does it match the style and density of the surrounding comments? [R.comments.idiom](#r.comments.idiom), [R.comments.brevity](#r.comments.brevity)

Second pass, which quotes each comment that the first pass keeps:

- Does every sentence follow the prose rules? [R.prose](#r.prose)

**Each paragraph of documentation**

- Does it describe the system as it is? [R.documentation-accuracy](#r.documentation-accuracy)
- Is it the one place that explains its topic, with other places linking to it? [R.documentation.locations](#r.documentation.locations)
- Does every sentence follow the prose rules? [R.prose](#r.prose)
- If it gives build or check instructions, does it sit with the component they apply to? [R.checking-instructions](#r.checking-instructions)

<a id="r.documentation-accuracy"></a>**[R.documentation-accuracy](#r.documentation-accuracy). Keep comments and documentation accurate to the current system.**

*Required. Principles [Coherence](PRINCIPLES.md#coherence), [Verification](PRINCIPLES.md#verification).*

Readers should be able to rely on descriptions of the system without knowing an earlier implementation. Describe current behavior, constraints, and lasting reasons. Put accounts of what changed and why in change records. Placement and duplication follow [R.documentation.locations](#r.documentation.locations).

## General writing

As general writing guidance, write for readers who do not share your context. Explain what the surrounding artifact cannot readily show. The rules below make sentence structure, terminology, and punctuation easier to follow.

<a id="r.prose"></a>**[R.prose](#r.prose). Prose clarity**

*Default. Rules [R.documentation-accuracy](#r.documentation-accuracy), [R.commit-explanations](4-history.md#r.commit-explanations), [R.pr-explanations](modules/pr.md#r.pr-explanations).*

Apply these rules to prose sentences.

**Sentence structure**

<a id="r.prose.focus"></a>**[R.prose.focus](#r.prose.focus). Keep one main idea per sentence.** Split sentences that make separate claims readers need to assess independently.

<a id="r.prose.flow"></a>**[R.prose.flow](#r.prose.flow). Order information from familiar context to new information.** Readers should be able to follow the sentence from left to right.

<a id="r.prose.subject-verbs"></a>**[R.prose.subject-verbs](#r.prose.subject-verbs). Keep subjects close to their verbs.**

**Actors and references**

<a id="r.prose.actors"></a>**[R.prose.actors](#r.prose.actors). Make clear who or what performs each action.** Name the actor when the sentence would otherwise leave it unclear. Assign actions to the entities that actually perform them.

<a id="r.prose.pronouns"></a>**[R.prose.pronouns](#r.prose.pronouns). Use pronouns only when their referents are clear.** Repeat a name when a pronoun could refer to more than one entity.

<a id="r.prose.explicit-nouns"></a>**[R.prose.explicit-nouns](#r.prose.explicit-nouns). State what is being described or compared.** Include the noun when readers would otherwise have to guess what has the stated property.

<a id="r.prose.modifiers"></a>**[R.prose.modifiers](#r.prose.modifiers). Place descriptive phrases next to the words they describe.** Rewrite a phrase when readers could connect it to the wrong person or thing.

**Word choice**

<a id="r.prose.terms"></a>**[R.prose.terms](#r.prose.terms). Build explanations from common words and from concrete names in the material.** Avoid technical jargon. When a technical term is necessary, define it in plain words before relying on it. For established project terms, link an existing definition when needed.

<a id="r.prose.hyphenation"></a>**[R.prose.hyphenation](#r.prose.hyphenation). Avoid invented hyphenated compounds.** State the action or relationship in an ordinary phrase. For example, prefer "selects the first successful alternative" to "first-success selection". Established compounds and standard prefixes are acceptable when they read naturally. Preserve hyphens in identifiers, URLs, proper names, and exact quotations.

<a id="r.prose.literal-language"></a>**[R.prose.literal-language](#r.prose.literal-language). Prefer literal descriptions to metaphors.** Use the actual operation, constraint, or relationship when a metaphor would leave readers to infer the meaning.

**Punctuation**

These punctuation choices support [one main idea per sentence](#r.prose.focus) and [the progression from familiar to new information](#r.prose.flow).

<a id="r.prose.punctuation"></a>**[R.prose.punctuation](#r.prose.punctuation). Replace semicolons, em dashes, and colons that join statements with clearer punctuation or separate sentences.** Use periods, commas, or parentheses according to the relationship being expressed. A colon may introduce a list. Preserve punctuation required by code, URLs, message syntax, source references, and exact quotations. `[auto, semicolons and em dashes only]`

<a id="r.prose.parentheses"></a>**[R.prose.parentheses](#r.prose.parentheses). Prefer parentheses only for brief qualifications.** Put a separate claim or an essential step in the explanation in its own sentence.

## Comments

<a id="r.comments.purpose"></a>**[R.comments.purpose](#r.comments.purpose). Use comments for constraints and reasons absent from the code.**

*Default. Principle [Coherence](PRINCIPLES.md#coherence). Rule [R.documentation-accuracy](#r.documentation-accuracy).*

Names, types, and implementation often supply the explanation. Add a comment when a constraint or reason is not evident from them. Accounts of what changed and why belong in change records under [R.documentation-accuracy](#r.documentation-accuracy).

Before adding a comment, consider whether a clearer name, smaller function, or stronger type can express the information. Omit comments that only paraphrase code, repeat a name, or label the next block.

A reader should be able to understand a comment without seeing an earlier version of the code.

<a id="r.comments"></a>**[R.comments](#r.comments). Comment placement and idiom**

*Default. Rule [R.documentation-accuracy](#r.documentation-accuracy).*

<a id="r.comments.definitions"></a>**[R.comments.definitions](#r.comments.definitions). Use function definition comments for caller-visible facts not evident from the signature.** For example, explain a required input order here.

<a id="r.comments.bodies"></a>**[R.comments.bodies](#r.comments.bodies). Use function body comments for non-obvious constraints or choices.** These can explain invariants, external constraints, specification rules, or implementation choices.

<a id="r.comments.idiom"></a>**[R.comments.idiom](#r.comments.idiom). Match the surrounding code's comment style and density.**

<a id="r.comments.placement"></a>**[R.comments.placement](#r.comments.placement). Place comments beside the code they explain.** Refer to identifiers visible at that location so readers can connect the explanation to the code.

<a id="r.comments.callers"></a>**[R.comments.callers](#r.comments.callers). Put caller-specific explanations at the caller.** A condition specific to one use belongs beside that use. A condition all callers must satisfy belongs in the function's contract.

<a id="r.comments.interfaces"></a>**[R.comments.interfaces](#r.comments.interfaces). Put caller-facing explanations in interface documentation when a separate interface exists.** Readers should find the contract where they look up the operation.

<a id="r.comments.brevity"></a>**[R.comments.brevity](#r.comments.brevity). Prefer brief comments.** As guidance, one sentence often suffices. If a comment needs several sentences, consider whether clearer names, a smaller function, or a stronger type could express some of the information. Keep the explanation when the code cannot express it.

## Documentation

<a id="r.documentation.locations"></a>**[R.documentation.locations](#r.documentation.locations). Give each explanation an authoritative home by default.**

*Default. Principle [Coherence](PRINCIPLES.md#coherence). Rule [R.documentation-accuracy](#r.documentation-accuracy).*

Link to the explanation instead of maintaining competing copies. Put setup and usage guidance in the relevant README, and keep component-specific details near the component.

Comments and documentation describe the current system under [R.documentation-accuracy](#r.documentation-accuracy).

### Markdown presentation

<a id="r.markdown-wrapping"></a>**[R.markdown-wrapping](#r.markdown-wrapping). Do not hard-wrap Markdown paragraphs or bullet text.** `[auto]`

*Default. Principles [Coherence](PRINCIPLES.md#coherence), [Proportionality](PRINCIPLES.md#proportionality).*

Keep each paragraph or bullet's text on one source line and let the renderer wrap it. Preserve line breaks required by code blocks, tables, or other Markdown structure. This also applies to PR bodies.

### Build and checking documentation

<a id="r.checking-instructions"></a>**[R.checking-instructions](#r.checking-instructions). Keep build and checking instructions with the component they apply to.**

*Default. Rule [R.documentation-accuracy](#r.documentation-accuracy).*

Document formatter versions, commands, and prerequisites in the relevant component guide. Link those instructions instead of maintaining another command list here. The [SpecTec module](modules/spectec.md#spectec-build-and-checks) provides compiler command recipes.
