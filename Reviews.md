# Reviews

These are just the general guidelines and the most important bits that will be
considered when reviewing contributions to a project. They are not exhaustive,
and final decisions may be different on a case-by-case basis, but they outline
the philosophy that goes under reviews, both for giving and receiving reviews.

# Protocol

## Reviewers: Be explicit

If you are the owner of the code in question,
**make a decision and tell the author explicitly**.

Do not make passive-aggressive suggestions such as "why don't you do it this way?".

Be explicit: tell them what can be changed, what is or isn't acceptable.
If something is unlikely to be accepted, tell them. If you can't make a decision
tell them to wait.

Either way, it's your responsibility to make a decision such
that the author knows exactly, in no uncertain terms, what to do next.
Do not keep pressing the author for more: They did 99% of their job when they
proposed the changes.

If you are not the owner of the code, do not make anything more than
suggestions. Do not give the author a hard time for not accepting your
suggestions. Do not keep pressing them.

## Reviewees: Accept consistency

If you are being reviewed, accept the fact that consistency is valued.
This includes style, choice of constructs, general structure, etc.
You are free to suggest deviations, but it's your responsibility to
explain why the inconsistency needs to be introduced.

If and when inconsistency is pointed out, you should generally accept
the changesuch that it's more consitent with the rest of the code.

Tip: it's generally more acceptable to be inconsistent in implementation
details than the API design/usage.

## Reviewees: Accept verification requests

If you are being reviewed, accept the fact that the reviewers don't
know what your code does, or if it does it correctly. It's your job
to provide proof via tests and documentation.

# Coding

* API design/usage is the most important, and will be under heavy scrutiny
* Value consistency than efficiency; if going for efficiency, take extra time to explain and test
* Be careful doing line-by-line reviews

## API Design/Usage

It's hard to describe how API design and usage matters, because it's fundamental
to all programming. After all, when we write a new function, we are introducing
a new API; when we call a function from another library, we are using an API.
It's all over the place, and in many contexts. So the following will be a bit
unorganized, but please bear with us.

### New APIs

When introducing new APIs (ones that you write for the project), consider the following:

**Are they named appropriately?** Are the names _specific_ enough, but _succinct_ enough?

**Are they properly exposed (public vs private)?** In general private APIs matter less,
as it can be tweaked later. Public APIs are there to stay, and therefore you will
have to take far more care in designing them.

### General Considerations

* APIs should be designed such that the default calling style satisfies 80-90% of the use cases, but should be extensible/flexible enough for the rest of relatively rare use cases.
* Carefully decide on mandatory arguments, optional arguments, and return values.
* Avoid creating public APIs that can't be invoked standalone, for they become liability later.
* Do not incorporate API usage that that perform similar tasks yet with a different calling conventions. For example, for new APIs there should be _one_ true way to perform the tasks (possible exceptions: utility methods that incorporate some default arguments). For using APIs, for example if you are creating text, do not mix `io.Writer` operations with `text/template`. If you do, there must be a clear reason/explanation why.

