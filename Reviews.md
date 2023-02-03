# Reviews

These are just the general guidelines and the most important bits that will be
considered when reviewing contributions to a project. They are not exhaustive,
and final decisions may be different on a case-by-case basis, but they outline
the philosophy that goes under reviews, both for giving and receiving reviews.

The main goals for having this guidelines are as follows:

* Reduce uncertainty between participants
* Reduce amount of communication neccessary to decide if a change goes in (or how it goes in)

# Protocol

## Reviewers: Be explicit

If you are the owner of the code in question,
**make a decision and tell the author explicitly**.

Do not make passive-aggressive suggestions such as "why don't you do it this way?" (i.e. It sounds like something the reviewee could say no to, but in fact you the reviewer is explicitly asking for a change).

Be explicit: tell them what can be changed, what is or isn't acceptable.
If something is unlikely to be accepted, tell them. If you can't make a decision
tell them to wait.

Either way, it's your responsibility to make a decision such
that the author knows exactly, in no uncertain terms, what to do next.
Do not keep pressing the author for more: They did 99% of their job when they
proposed the changes. Do not engage in lengthy discussions that forces the
author to spend more time debating: again, they did 99% of their job when
they proposed the changes. It's your reponsibility to make a decision.

If you are not the owner of the code, do not make anything more than
suggestions. Do not give the author a hard time for not accepting your
suggestions. Do not keep pressing them.

## Reviewees: Rejection is allowed, but it goes both ways

Sometimes reviewers may ask for changes that you whole-heartedly do not agree with.
You have the right to reject them. In fact, if you are the code owner, you
should refer to [the previous section](#reviewers-be-explicit) and **make a decision**
to accept or reject the suggestions.

If you are not a code owner, you also have the right to object, but you should
ultimately accept that it's the code owners' right and responsibility to 
decide if a particular request for change is a show-stopper or not.
The code owners have the right to reject your rejection. Do not engage in
prolonged discussions for rebuttal and make the reviewer spend more time.

## Reviewers: Line-by-line scrutiny is generally not necessary

We would rather have more tests or documentation than have the reviewer
spend time with line-by-line reviews. In a similar manner, we would
rather have the authors spend more time writing tests and documents
than answering each critique.

This is not to say that we don't or shouldn't check for code. It
just means that the fact that the existence of intent (documentation) and 
verification (tests) are far more important than, for example,
if a loop is tight enough.

If you are doing nitpick reviews, try to use the `suggestion` feature
as much as possible, so that the author(s) can just accept your code changes
instead of having to (possibly) second guess what your review intentions
are, further increasing the communication costs.

## Reviewees: Accept consistency

If you are being reviewed, accept the fact that consistency is valued.
This includes style, choice of constructs, general structure, etc.
You are free to suggest deviations, but it's your responsibility to
explain why the inconsistency needs to be introduced.

If and when inconsistency is pointed out, you should generally accept
the change such that it's more consitent with the rest of the code.

Tip: it's generally more acceptable to be inconsistent in _implementation_
details than the _API_ design/usage.

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
It's all over the place, and in many contexts.

But fundamentally, we take the API as a _contract_. A contract could be an agreemnt
between a person to a person, but in context of code, we're dealing with
potentially a lot of people. And therefore we believe that the API is the hardest part
to change in a code. This applies for both designing new APIs, and consuming APIs 
(potentially from other libraries) within the code.

In contrast, specific implementations can be improved/fixed/changed later without
changing the API (given that the API was designed properly).

Therefore, the APIs you create, and the APIs you choose to use are going to be
scrutinized.

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

