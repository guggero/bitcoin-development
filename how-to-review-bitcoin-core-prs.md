## How to Review Bitcoin Core PRs

Last updated: January 20, 2020

*Hi! This article now lives at
[https://jonatack.github.io/articles/how-to-review-pull-requests-in-bitcoin-core](https://jonatack.github.io/articles/how-to-review-pull-requests-in-bitcoin-core).
I will continue to update it there. Cheers.*


### BEFORE YOU BEGIN

This guide builds on the foundation laid by these presentations:

1. [A Gentle Introduction to Bitcoin Core Development](https://bitcointechtalk.com/a-gentle-introduction-to-bitcoin-core-development-fdc95eaee6b8)
by [Jimmy Song](https://twitter.com/jimmysong) (2017)

2. [Contributing to Bitcoin Core, a personal account](https://bitcointechtalk.com/contributing-to-bitcoin-core-a-personal-account-35f3a594340b)
by [John Newbery](https://twitter.com/jfnewbery) (2017)

3. [Understanding the Technical Side of Bitcoin](https://medium.com/@pierre_rochard/understanding-the-technical-side-of-bitcoin-2c212dd65c09)
by [Pierre Rochard](https://twitter.com/pierre_rochard) (2018)

4. [A hardCORE workout](https://www.youtube.com/watch?v=MJBhZg0ytiw)
   /
   [transcript](http://diyhpl.us/wiki/transcripts/sf-bitcoin-meetup/2018-04-23-jeremy-rubin-bitcoin-core/)
   /
   [slides](https://drive.google.com/file/d/149Ta1WRXL5WEvnBdlL-HxmsFDXUbvFDy/view)
   by [Jeremy Rubin](https://twitter.com/JeremyRubin) (2018)


### INTRODUCTION

*"Reviewing is the most effective way you can contribute as a new contributor
(and also will teach you much more about the code than opening PRs)."*

&mdash; John Newbery, Bitcoin Core PR Review Club meeting, 5 September 2019

Reviewing and testing can be the best ways to begin contributing to Bitcoin
Core.

Experienced review and testing are regularly cited by long-term Bitcoin Core
developers as both

  - resource bottlenecks, and

  - the best and most helpful way to begin contributing and earning reputation
    in the community.

Yet the process and learning curve can seem intimidating and in practice very
few new contributors do it.

As a newcomer, this article represents my current understanding after a few
months, a few dozen PR reviews, a few issues tested or handled, and a handful of
commits.

Some of this understanding was gained from

  - contributing to a large open source project,
    [Ruby on Rails](https://github.com/rails/rails), and co-editing its blog and
    newsletter, [This Week in Rails](https://rails-weekly.ongoodbits.com/archive)

  - development and lead maintainership of
    [Ransack](https://github.com/activerecord-hackery/ransack),
    a popular Ruby search engine

  - daily discussions on this topic of mutual interest with my good friend and
    colleague, [Kasper Timm Hansen](https://twitter.com/kaspth), a developer at
    [Basecamp](https://basecamp.com/about/team) and since 2016 a member of the
    [Ruby on Rails Core Team](https://rubyonrails.org/community/).

Yet much of it is unique to Bitcoin Core and came only with time. I would have
preferred to know these things from the start. So here we are. This is foremost
a self-study exercise, but perhaps it can be useful for others.

### TERMINOLOGY

[PR](https://help.github.com/en/articles/about-pull-requests): An acronym for
*pull request*, sometimes called a merge request. A proposed change to the code
or documentation in the source code repository.

[WIP](https://en.wikipedia.org/wiki/Work_in_process): An acronym for *work in
progress*.

[ACK, NACK, nit](https://github.com/bitcoin/bitcoin/blob/master/CONTRIBUTING.md#peer-review):
Defined [here](https://github.com/bitcoin/bitcoin/blob/master/CONTRIBUTING.md#peer-review).


### GENERAL

As a newcomer, the goal is to try to add value, with friendliness and
humility, while learning as much as possible.

A good approach is to make it not about you, but rather "How can I best serve?"

One of the most challenging aspects facing new contributors is the breadth of
the codebase and the complexities of the technologies surrounding it.

Be aware of what you don’t know; long-term contributors have years of experience
and context. The community has built up a deep collective wealth of knowledge
and experience. Keep in mind that your new ideas may have already been proposed
or considered several times in the past.

Remember that contributor and maintainer resources are limited -- ask for them
carefully and respectfully. The goal is to try to give more than you take, to
help more than hinder, while getting up to speed.

Try to figure things out on your own, at least sufficiently to respect others'
time.

Follow the
[#bitcoin-core-dev](https://webchat.freenode.net/?channels=bitcoin-core-dev)
IRC channel and the
[bitcoin-dev](https://lists.linuxfoundation.org/mailman/listinfo/bitcoin-dev)
mailing list.

More IRC channels to follow can be found
[here](https://github.com/jonatack/bitcoin-development/blob/master/irc-channels.txt).

Before jumping in, take plenty of time to:

  - understand the contribution process and guidelines, not only by reading
    the documentation in the [repository](https://github.com/bitcoin/bitcoin),
    notably
    [Contributing to Bitcoin Core](https://github.com/bitcoin/bitcoin/blob/master/CONTRIBUTING.md)
    and everything in the
    [doc](https://github.com/bitcoin/bitcoin/tree/master/doc) and
    [test](https://github.com/bitcoin/bitcoin/tree/master/test)
    [directories](https://github.com/bitcoin/bitcoin/tree/master/src/test),
    but also by observing interactions on the
    [#bitcoin-core-dev](https://webchat.freenode.net/?channels=bitcoin-core-dev)
    IRC channel and the ongoing
    [code review in the repository](https://github.com/bitcoin/bitcoin/pulls)

  - get to know the maintainers and regular contributors: what they do, what
    they like and want, how they give feedback

Participate in the excellent [Bitcoin Core PR Review
Club](https://bitcoincore.reviews) weekly meetings on IRC. The club was launched
in May 2019 by [John Newbery](https://twitter.com/jfnewbery). You'll benefit the
most if you prepare for each meeting in advance by studying, building, and
testing the PR under review -- and then actually reviewing it! Go through the
notes, questions, and logs of the previous meetings; there is gold in there.

Many newcomers begin by filing pull requests that add to the hundreds already
awaiting valuable review. In many cases, it may be better to begin by reviewing
the existing pull requests and starting to understand what kind of pull
requests and review are most helpful, while slowly gaining the big picture.

#### The Big Picture

The big picture is more important than nits, spelling, or code style.

Steps to improve understanding of the big picture:

- do the [Chaincode Labs study guide](https://github.com/chaincodelabs/study-groups)

- read and do [Programming Bitcoin](https://github.com/jimmysong/programmingbitcoin)

- study the [Bitcoin Improvement Proposals](https://github.com/bitcoin/bips/)
  (often referred to in singular form by the acronym "BIP"), and return to them
  frequently

- subscribe to the [Bitcoin Optech newsletters](https://bitcoinops.org/) and
read their [Scaling Book](https://github.com/bitcoinops/scaling-book)

- do [Learning Bitcoin from the Command Line](https://github.com/ChristopherA/Learning-Bitcoin-from-the-Command-Line)

Aim for quality over quantity and a balance between deep work and quick wins.

Documentation is important, e.g. high-level documentation of how things work and
interact, clear and accurate code docs, whether a function has a good
description and [Doxygen
documentation](https://github.com/bitcoin/bitcoin/blob/master/doc/developer-notes.md#coding-style-doxygen-compatible-comments),
test logging (both `info` and `debug`), and so on.

Test coverage is essential; don't hesitate to improve or write any missing
[unit](https://github.com/bitcoin/bitcoin/blob/master/src/test/) or
[functional](https://github.com/bitcoin/bitcoin/tree/master/test/functional/)
tests.

Be a contributor. Help PRs move forward by reviewing, [proposing
tests](https://github.com/bitcoin/bitcoin/pull/15996#issuecomment-491740946) or
fixes in a helpful way, proposing to rebase, or even offering to take over the
PR after months of silence. In short, help each other!

#### Nits

Try to avoid overly commenting in PRs about nits, minutia and code style,
particularly with PRs labeled as WIP, or when a PR has just been filed and the
PR author is mainly looking for Concept ACKs and Approach ACKs, e.g. general
consensus, not nitpicking.

Long-term contributors report that activity like this repels them, and it can
diminish your social capital on the project. Try to understand what kind of
review is needed and when to do what.

The best time for any nit comments is after the Concept/Approach ACKs and
consensus on the PR, and before the PR is finalised and has tested ACKs.

Give nits and style advice in a friendly, light, enabling way -- as in, feel
free to ignore, feel free to adjust if you happen to rebase, etc.

Keep in mind that no one is forced to take your review comments into account;
it's perfectly fine for the author to reply that they don't want to do something
if they feel it is outside the scope of the change, especially if your comment
is nitpicky.

#### Scale Up

When you can, scale up the difficulty and priority of the PRs you review.

You can add more value and learn more by taking the time to do deep, quality
review of the [high-priority PRs](https://github.com/bitcoin/bitcoin/projects/8)
and the more difficult PRs. These PRs tend to intimidate people and can stagnate
for months, killing their author's motivation with death by a thousand cuts from
lack of quality review, nitpicking/code style bikeshedding, and rebase hell.
Reviewing them well provides a true service to Bitcoin.

The process of ramping up takes time; nothing can substitute for months and
years invested in gathering context and understanding from following the
[code](https://github.com/bitcoin/bitcoin),
[issues](https://github.com/bitcoin/bitcoin/issues),
[pull requests](https://github.com/bitcoin/bitcoin/pulls),
[#bitcoin-core-dev](https://webchat.freenode.net/?channels=bitcoin-core-dev)
IRC channel, and the
[bitcoin-dev](https://lists.linuxfoundation.org/mailman/listinfo/bitcoin-dev)
mailing list.

#### Step by Step

Keep ego and hopes out of the process. Don't take things personally and keep
moving forward.

When in doubt, assume good intentions.

Be patient with people and outcomes.

Persistence helps. Work on it every day.

These are all much easier said than done. Be forgiving with yourself and others.

John Newbery:

- A good rule of thumb is to review 5-15 PRs for each PR you make
- Start small
- Have a plan, don't spread yourself too thin
- Sharpen your tools
- Ask for and offer help, like rebasing for people or adding test cases
- People are generous with their time because they care
- Contribute by understanding what others want and being respectful


### TECHNICAL SPECIFICS

*Don't trust, verify.* Minimise dependance on GitHub in your review process. Use
the GitHub website only for the GitHub metadata, e.g. reading comments and
adding your own comments -- not for reviewing the commits and code, which you
should do in your local environment.

Therefore, a review begins by pulling the PR branch down to your computer to
build and review locally. There are several ways to do it:

- Bitcoin Core documentation for [referencing PRs easily with
  refspecs](https://github.com/bitcoin/bitcoin/blob/master/doc/productivity.md#reference-prs-easily-with-refspecs)
- Pulling down remote PRs with `git checkout pr/<number>` [as described in this nice
  little gist](https://gist.github.com/piscisaureus/3342247)
- GitHub now [exposes
PRs](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/checking-out-pull-requests-locally)
as branches on the upstream repository with `git pull/<number>/head` (contributor
branch) and `git pull/<number>/merge` (merged into master), e.g. `git fetch origin
pull/17283/head && git checkout FETCH_HEAD`

You can test a PR either on the contributor's branch or with the changes merged
on top of master. Testing the latter can be useful to see if anything merged
into master since the last PR commit breaks the changes.

Next, launch the build and tests while you begin reading the code
locally. You'll need to become comfortable with [compiling Bitcoin Core from
source](https://github.com/jonatack/bitcoin-development/blob/master/how-to-compile-bitcoin-core-from-source-on-linux-and-macOS.md)
and running the [unit
tests](https://github.com/bitcoin/bitcoin/tree/master/src/test/README.md) and
[functional
tests](https://github.com/bitcoin/bitcoin/blob/master/test/README.md) since you
will need to do it for most of the PRs you test. For this, the Bitcoin Core
[productivity
notes](https://github.com/bitcoin/bitcoin/blob/master/doc/productivity.md) are
indispensable.

While the build and tests are running, begin reviewing each commit separately in
your local environment using a difftool like
[gitk](https://git-scm.com/docs/gitk), [meld](https://meldmerge.org/), [meld for
macOS](https://yousseb.github.io/meld/),
[GNU](https://www.gnu.org/software/emacs/manual/html_node/ediff/index.html)
[ediff](https://www.emacswiki.org/emacs/EdiffMode),
[vimdiff](https://vim.fandom.com/wiki/A_better_Vimdiff_Git_mergetool), or
opendiff on macOS. If you use gitk and like dark mode, I recommend [Dracula for
gitk](https://github.com/dracula/gitk).

Become adept at searching the repository with `git grep`. You'll use it
constantly. Run `git grep --help` on the command line for help or information.

Read and know the Bitcoin Core [developer
notes](https://github.com/bitcoin/bitcoin/blob/master/doc/developer-notes.md).

#### If You're Not Sure Where to Start

Read the code, read the PR comments, then re-read both. Find something that
doesn't make sense and try to figure it out. Repeat.

Once it all starts to make sense, run bitcoind on testnet (or on mainnet with
very small amounts), and tail or search through the relevant logs (run
`bitcoin-cli help logging` for the various bitcoind logging categories and how
to toggle them on/off).

Maybe add some custom logging, LogPrintfs, or asserts; it's always a privilege
to add these into other people's code (to see how, run `git grep -ni logprintf`
or `git grep assert` in the repository).

Run the relevant functional tests and look through the debug logs. Verify that
they fail in the expected way on master. Back in the PR branch, inverse or
change the new tests to make them break and understand why.

Maybe add C++ gdb or Python pdb breakpoints. Examine values. Run RPC commands.

Check if any call sites, headers or declarations have been overlooked in the PR.

Try refactoring the code to be better or prettier, and discover why that doesn't
work. Expect it to take twice as long as you planned it to. Yes, it's work.

#### Add missing tests

While you're reviewing, writing tests yourself can help you understand the
behaviour and verify the changes, and if they add useful coverage you can
propose them to the author for inclusion in the PR. Proposing automated tests is
a really helpful way to start contributing. Authors appreciate it when someone
reviews their PR and provides additional tests. [Here's an
example.](https://github.com/bitcoin/bitcoin/pull/15996#issuecomment-491740946)

#### Big picture > nits

Remember, the big picture is much more important than nits, spelling, or code
style. Re-read the [Nits](#nits) section above. Try to avoid commenting on these
while reviewing, even if you have no other comments to make. I know, it's hard
-- I've done it too many times -- but there's a better alternative:

#### Ask Questions

A good thing you can do as a reviewer without specialised knowledge of the code
is _ask questions_. A PR author is usually happy to discuss their work or see
interest in it. So, spend 20 minutes or so looking at a change, find the thing
that seems most confusing or surprising, and ask about it politely in the PR
comments or on the
[#bitcoin-core-dev](https://webchat.freenode.net/?channels=bitcoin-core-dev) IRC
channel. Chances are other people wonder about the same thing and it could be
clarified or documented better. In this way you can learn and help make the
project more accessible, too. (Credit for this paragraph: [Russell
Yanofsky](https://github.com/bitcoin/bitcoin/pull/15934#issuecomment-547095024)).

#### Peer Review

Be sure to learn and understand the Bitcoin Core [peer review
process](https://github.com/bitcoin/bitcoin/blob/master/CONTRIBUTING.md#peer-review).
The process is [often](https://github.com/bitcoin/bitcoin/pull/15626)
[updated](https://github.com/bitcoin/bitcoin/pull/16149), so refer back to it
frequently.

Concept ACK means the reviewer acknowledges and agrees with the goal of the
change, but is not (yet) confirming they've looked at the code or tested it.
This can be a valuable signal to a PR author to let them know that the PR has
merit and is headed in the right direction. As a corollary, a Concept NACK would
indicate disagreement with the goal.

Approach ACK is a step further than Concept ACK and means agreement with both
the goal and the approach used in implementing the change. Approach NACK would
therefore indicate agreement with the goal but not the approach.

Manual testing of new features and reported issues is always welcome. A comment
that is really helpful in review: "Here's what I tested and my methodology",
particularly to back up an ACK.

Some PRs can be difficult to test or ACK due to complexity, context, or possibly
a lack of tests or simulation framework. That shouldn't discourage you from
reviewing. For example, if you've reviewed the code thoroughly, a comment like
"the code looks correct to me, but I don't feel confident enough about behaviour
to give an ACK" is a perfectly helpful contribution.

When giving an ACK, specify the commits reviewed by appending the commit hash of
the `HEAD` commit. The trustless way to do this is to use the hash from your
*local* checkout of the branch and not from the GitHub web page. That way,
unless your local tools are compromised, you ensure you are ACKing the exact
changes. This is also useful when a force push happens and links to old commits
are lost on GitHub.

A full ACK could look like: "ACK `fa2f991`, I built, ran tests, tested manually
by doing X/Y/Z and reviewed the code and it looks OK, I agree it can be merged."

The Bitcoin Core merge script currently copies into the merge commit all ACK
comments pertaining to the `HEAD` commit at the time of merge. Keep in mind that
anything you write in an ACK comment that is copied by the merge script will be
in git history forever.

Some Bitcoin Core contributors sign and OpenTimestamp their ACKs. While that is
beyond the scope of this document, it is surprisingly trivial to sign your
commits using the [OpenTimestamps Git
Integration](https://github.com/opentimestamps/opentimestamps-client/blob/master/doc/git-integration.md).

Bitcoin Core reviewers frequently use the [Apache voting
system](https://www.apache.org/foundation/voting.html#expressing-votes-1-0-1-and-fractions)
in their comments. Here is an
[example](https://github.com/bitcoin/bitcoin/pull/11426#issuecomment-334091207).

As a new contributor, be cautious with giving a NACK. Assume by default that you
might lack understanding or context. If you do NACK, provide good reasoning.
[Here's one
example.](https://github.com/bitcoin/bitcoin/pull/12360#issuecomment-383342462)

When you disagree, state your point of view once and move on. Don't flood the
comments section, browbeat others or overreact. Remember that the most
important thing is probably not the issue being discussed, but your relationship
with the other contributors.

A complex PR usually requires at least 3-4 experienced ACKs before merging.

#### Miscellaneous Technical Advice

fanquake:
- I have some core dev tools in https://github.com/fanquake/core-review
  It has guides on how to gitian build, review certain types of PRs, etc
  I still need to improve the docs and push up more stuff I have sitting locally
- There is also https://github.com/bitcoin-core/bitcoin-maintainer-tools
- Rough distro list for build-related changes:
  https://github.com/fanquake/core-review/blob/master/operating-systems.md

harding:
- In case it's helpful to anyone, I took a quick look at the PR and
[made notes about my review process and what I'd test
for](https://gist.github.com/harding/168f82e7986a1befb0e785957fb600dd)

harding's process:
1. Open PR in browser
2. Checkout PR in dev environment
3. Build
4. Run integration tests
5. During and after 2-4, make notes on what I need to review
6. Answer what questions I can by looking at the code
7. Start regtest node (or testnet or mainnet if necessary) and review actual
   operation matches my expectation from the code

John Newbery:

I always download the PR branch to my machine so I can build and review locally.
I don't use the github webpage to review, only to leave comments.

My git tools: https://gist.github.com/jnewbery/1d45a6b5e14b3f3fefe5942d0cc2608d

I've got a short script that checks out the PR branch and queries the github API
to add a description to that branch locally, that makes it easier when I have a
bunch of PRs checked out locally that I can run a `git branch` command and see
what they are

once I have the branch locally, I'll set off a build in a VM while I look
through the changes

first, I run something like `git log --oneline upstream/master..`
that gives me a list of all the commits in the PR branch, one per line

and then I use a one-liner, which I have bash aliased as git-review, that steps
through the commits one-by-one, printing the commit log to the console, then
opening my difftool program:

for commit in `git log master..HEAD --oneline | cut -d' ' -f1 | tac`; do git log -1 $commit; git difftool ${commit}{^,} --dir-diff; done

I'll look at the diff, and when I quit the difftool program, git-review will
step forward to the next commit

First run through, I'll just skim everything, reading the commit logs and
looking at the overall changes, so I get an idea of what the PR is doing

Then I'll go through again, but look at each commit in more detail,
reviewing every line in detail

I make extensive use of the functional tests by adding
`import pdb; pdb.set_trace()`
break points, and then manually running RPC commands on the nodes under test

I pull the PR description from the github API and then use it to label the branch

There's an attribute of a git branch called `description` that you can update
manually, my `gb` doesn't map onto `git branch` exactly, I do some formatting on
the output so it includes the description

I'm using vagrant, just the standard ubuntu bionic image.
I have a vagrant file that installs all the dependencies.

I run make check and the functional tests, not usually --extended because I'm
too impatient.

Here's my vagrant config (YMMV): https://github.com/jnewbery/btc-dev

A toolchain for bitcoind data files: https://github.com/jnewbery/bitcointools

MarcoFalke: to run functional tests in the gui, pass BITCOIND=bitcoin-qt

To turn on debug=net with the logging RPC: bitcoin-cli logging '["net"]'

If we need any more linters it should be to check for unexpected changes to
consensus code


### BOOKS

#### C++ Books

Bitcoin Core is written in C++ 11. Here are some C++ book recommendations:

The Reference

- [The C++ Programming Language, 4th Edition](https://www.amazon.com/Programming-Language-hardcover-4th/dp/0321958322)

Learning C++

- [C++ Primer, 5th Edition](https://www.amazon.com/Primer-5th-Stanley-B-Lippman/dp/0321714113/)
  (more gentle, longer, not to be confused with the knock-off, "C++ Primer Plus")
- [Accelerated C++](https://www.amazon.com/Accelerated-C-Practical-Programming-Example/dp/020170353X/)
  (condensed, faster, a bit out of date but excellent,
  [exercise solutions here](https://github.com/bitsai/book-exercises/tree/master/Accelerated%20C%2B%2B))

Intermediate/advanced

- [Effective C++](https://www.amazon.com/Effective-Specific-Improve-Programs-Designs/dp/0321334876/)
- [Effective Modern C++](https://www.amazon.com/Effective-Modern-Specific-Ways-Improve/dp/1491903996/)
- [Effective STL](https://www.amazon.com/Effective-STL-Specific-Standard-Template/dp/0201749629/)
- [Exceptional C++](https://www.amazon.com/Exceptional-Engineering-Programming-Problems-Solutions/dp/0201615622/)
- [More Exceptional C++](https://www.amazon.com/More-Exceptional-Engineering-Programming-Solutions/dp/020170434X/)
- [C++ Templates: The Complete Guide (1st Edition)](https://www.amazon.com/Templates-Complete-Guide-David-Vandevoorde/dp/0201734842/)
- [C++ Templates: The Complete Guide (2nd Edition)](https://www.amazon.com/C-Templates-Complete-Guide-2nd/dp/0321714121/)
- [C++ Concurrency in Action, 2nd Edition](https://www.amazon.com/C-Concurrency-Action-Anthony-Williams/dp/1617294691/)

#### Cryptography

- [Foundations of Cryptography](https://www.amazon.com/Foundations-Cryptography-Basic-Tools-Vol-dp-0521791723/dp/0521791723/)
- [Waxwing's blog](https://joinmarket.me/blog) by the JoinMarket creator and
    cryptographer [Andrew Gibson](https://mastodon.social/@waxwing)
- [A Graduate Course in Applied Cryptography](https://crypto.stanford.edu/~dabo/cryptobook/BonehShoup_0_4.pdf)
    by [Dan Boneh](https://en.wikipedia.org/wiki/Dan_Boneh)
- [Cryptopals](https://www.cryptopals.com/) - A set of cryptographic code
    challenges


### CREDITS

A special thank you to [John Newbery](https://twitter.com/jfnewbery) for
launching the [Bitcoin Core PR Reviews Club](https://bitcoincore.reviews) and to
the long-term contributors who participated so far: [Dave
Harding](https://hash.social/users/harding), Anthony Towns, Gregory Sanders,
Michael Ford, Andrew Chow, Pieter Wuille, Bryan Bishop, Mike Schmidt, Marco
Falke, and Wladimir van der Laan.

Thanks to [Steve Lee](https://twitter.com/moneyball) (moneyball) for reviewing
this write-up and his suggestions.

This article includes observed comments on GitHub and IRC by the following
Bitcoin Core contributors/maintainers who deserve to be credited:
Wladimir van der Laan, Marco Falke, Pieter Wuille, Gregory Maxwell, Anthony
Towns, and Russell Yanofsky.

Over the years I had become disillusioned by the central influence of BDFLs in
programming languages and open source projects. Wladimir van der Laan's
[long-standing](https://twitter.com/orionwl/status/1131564038444453889)
[humble](https://twitter.com/orionwl/status/1131827793908645888)
[service](https://twitter.com/orionwl/status/1131924832071880705) to Bitcoin
sparked the possibility to me of perhaps doing the same.

Finally, a big thank you to the Bitcoin Core contributors for their patience
with my review attempts so far, notably John Newbery, Marco Falke, João Barbosa,
practicalswift, Gregory Sanders, Jonas Schnelli, Pieter Wuille and Wladimir van
der Laan, and to Adam Jonas and John Newbery for their guidance and advice from
the start.

Cheers,

Jon Atack
GitHub: https://github.com/jonatack
Twitter: https://twitter.com/jonatack
Mastodon: https://x0f.org/web/@jon
