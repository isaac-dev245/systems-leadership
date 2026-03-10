# Systems Leadership: Deming, RFC 1925, Unix Philosophy, and Cantrill

*A framework for leading complex sociotechnical systems*

---

## On the Structure of This Document

Bryan Cantrill draws a distinction between principles, values, and mission. Principles are universal truths, constraints on behaviour that hold true regardless of the context. Values are expressions of importance; priorities that define what you optimize for when forced to choose. Mission is the "why", it provides direction to both.

This matters because most organizations confuse the three. They write "values" statements full of principles, in the name of integrity, and subsequently principles that are full of values. If you treat a value as a principle, you stop making tradeoffs. If you treat a principle as a value, you end up negotiating with things that should not be negotiable.

Four traditions, developed independently across manufacturing, internet engineering, operating systems, and infrastructure compute, converge on remarkably similar insights about complex systems. W. Edwards Deming's management philosophy was realized through statistical quality control. RFC 1925 crystallized from hard-won lessons learned in building the Internet. The Unix Philosophy codified what made an OS survive across decades. Bryan Cantrill's body of work, from his development of DTrace at Sun Microsystems, through Joyent, and on to Oxide Computer, adds the connective tissues: why these insights are so hard to follow, and what it looks like when organizations actually live their values.

Together they form a framework for leading and managing complex systems. It applies to networks, datacenters, organizations, and the messy places where all three intersect.

---

## Part I: The Source Frameworks

### Deming's System of Profound Knowledge

Deming's management philosophy rests on four interconnected pillars, none of which functions without the others.

**Appreciation for a system.** A system is a set of interdependent components working towards a common aim. Optimizing individual components does not consider the whole, and as a result it often degrades it. The majority of problems belong to the system; most people are doing their best within the system itself. Most organizations invert this when assigning blame.

**Knowledge of variation.** All processes exhibit variation. Some are inherent to the system, some results from specific, identifiable factors. Confusing the two – reacting to common cause – makes systems worse. Tampering with a stable system by design introduces instability.

**Theory of knowledge.** Experience alone teaches nothing without theory. The Plan-Do-Study-Act cycle is Deming's method for building knowledge iteratively: plan the change, execute, study the results, act on what was learned.

**Psychology.** People are not interchangeable components. They have intrinsic motivation which typical management systems mostly destroy. Fear will drive out truth-telling. The job of management is to create conditions where people can DO good work.

Deming's 14 points for management create these pillars:

- Create constancy of purpose
- Cease dependence on inspection
- Improve constantly
- Drive out fear
- Break down barriers
- Eliminate slogans and exhortations
- Eliminate quotas
- Remove barriers to pride of workmanship
- Institute education
- Put everyone to work on the transformation

### RFC 1925: The Twelve Networking Truths

Published April 1, 1996, April Fools' Day, because the truths are funny right up until they aren't.

1. It Has to Work.
2. No matter how hard you push and no matter what the priority, you can't increase the speed of light.
   - No matter how hard you try, you can't make a baby in much less than 9 months. Trying to speed this up *might* make it slower, but it won't make it happen any quicker.
3. With sufficient thrust, pigs fly just fine. However, this is not necessarily a good idea. It is hard to be sure where they are going to land, and it could be dangerous sitting under them as they fly overhead.
4. Some things in life can never be fully appreciated nor understood unless experienced firsthand. Some things in networking can never be fully understood by someone who neither builds commercial networking equipment nor runs an operational network.
5. It is always possible to agglutinate multiple separate problems into a single complex interdependent solution. In most cases this is a bad idea.
6. It is easier to move a problem around than it is to solve it.
   - It is always possible to add another level of indirection.
7. It is always something.
   - Good, Fast, Cheap: Pick any two (you can't have all three).
8. It is more complicated than you think.
9. For all resources, whatever it is, you need more.
   - Every networking problem always takes longer to solve than it seems like it should.
10. One size never fits all.
11. Every old idea will be proposed again with a different name and a different presentation, regardless of whether it works.
    - See rule 6a.
12. In protocol design, perfection has been reached not when there is nothing left to add, but when there is nothing left to take away.

These truths were written about networking. They apply to every complex system humans have ever built.

### The Unix Philosophy

The Unix Philosophy emerged from the design of Unix at Bell Labs in the 1970s and was refined over decades by McIlroy, Thompson, Kernighan, Pike, and Raymond, among others. Its core tenets:

**Make each program do one thing well.** To do a new job, build fresh rather than complicate older systems by adding new "features".

**Expect the output of every program to become the input to another.** Don't clutter the outputs with trivial information, don't insist on interactive input.

**Design and build software to be tried early.** Don't hesitate to rebuild the clumsy parts

**Use tools in preference to unskilled help to lighten a programming task**, even if you have to detour to build the tools and expect to throw some of them out after you've finished using them.

The power of a system comes from the relationships among programs, rather than from the programs themselves. The philosophy favors composability over completeness, clarity of understanding over cleverness, and the assumption that today's work will need to change tomorrow.

Raymond later codified additional rules: the Rule of Modularity (write simple parts connected by clean interfaces), the Rule of Clarity (clarity is better than cleverness), the Rule of Separation (separate policy from mechanism), the Rule of Parsimony (write a big program only when nothing else will do), the Rule of Transparency (design for visibility to make inspection and debugging easier), and the Rule of Repair (when you must fail, fail noisily and as soon as possible).

### Cantrill: Values, Systems, and the Forgotten Operator

Bryan Cantrill's contributions span DTrace at Sun Microsystems, Joyent, and Oxide Computer, however his most broadly applicable ideas concern how organizations and technical systems embody values and what happens when they don't do, deliberately.

**Values as architecture.** Platforms, language, and organizations embed values, intentionally or not. Cantrill calls out a taxonomy of platform values: composability, debuggability, expressiveness, extensibility, interoperability, integrity, maintainability, measurability, operability, performance, portability, resiliency, rigor, robustness, safety, security, simplicity, stability, thoroughness, transparency, velocity. All are good things, and all are in tension with each other. A platform's core values are revealed through what it's forced to pick, not what it aspires to be. An organization that hasn't articulated which values it prioritizes when there are conflicts will produce incoherent systems because every team will resolve those tensions differently.

**The principles/values/mission hierarchy.** Principles are universal truths that hold as such across time, geography, culture, and context. They are constraints, not aspirations. Integrity, honesty, decency: these are principles. You either have them or you don't, they are not subject to tradeoffs. Values are where interesting decisions live: what do you optimize for when forced to choose between multiple good things? Mission is the animating purpose that provides direction to both. Most organizations conflate the three.

**Observability as a design requirement.** If the system cannot be observed you are reduced to guessing, making changes, and drawing inferences from correlation. That is not engineering. Systems must be instrumentable, capable of producing the data you need in the conditions in which you need it, without requiring advance predictions of what questions will be asked. DTrace was built on this premise. Oxide's entire stack reflects it.

**The forgotten operator.** The people and teams who run the system at 3am have been broadly ignored by an industry fixed on builders and buyers. On-premise operators, tasked with running elastic infrastructure on brittle hardware in their own datacentres, epitomize resourcefulness, often having to invent the missing software required to stitch together systems that were never designed to work together. Designing for these people means contemplating the entire lifecycle. It means empathy for the person who bears the consequences of your design decisions.

**Rigor over folklore.** Resist the temptation to change the system before understanding it. Resist jumping to hypotheses. Iterate between questions and the observations; gather facts that constrain future hypotheses. Get to the root of the problems, don't just address the symptoms.

**Co-design across boundaries.** The best systems come when components are designed to work together, not integrated after the fact. This applies to hardware, software, teams and organizations, to policy and mechanism. The cost of integration is lowest at design time and increases exponentially as systems mature independently.

---

## Part II: Principles

Principles are constraints. They hold true whether you acknowledge them or not. You don't choose them; you choose whether to respect them. These are the principles all four traditions converge on.

### It Has To Work

RFC 1925 puts this first for a reason. It is the constraint that precedes all others. A system that doesn't work is not simple, elegant, or well-architected. It is broken.

This sounds obvious, but it is not. Organizations routinely sacrifice "working" for "impressive", "compliant", or "on schedule". Deming's first point – constancy of purpose – exists because organizations lose sight of the purpose. Cantrill's insistence on rigor exists because people convince themselves that something is working, when it is not, because they've stopped looking closely enough to tell.

Every principle and value here is a subordinate to this one. If following a principle makes the system stop working, either the principle or the system has been misunderstood.

### Hard Constraints Are Real

The laws of physics are immutable. You cannot increase the speed of light, you cannot run an enterprise on infrastructure that doesn't exist, you cannot staff a project with people you haven't hired, and you cannot compress a 6-month migration into a sprint because a deadline moved.

Deming's knowledge of variation formalizes this: systems have inherent limits and treating those limits as problems to be solved rather than constraints to be respected makes everything worse. The Unix philosophy embeds it with the preference for small tools – don't build more than the space allows. Cantrill's philosophy accepts it: if you can't change the constraint, design the system to work within it rather than ignoring it.

With sufficient thrust, pigs fly just fine. But knowing where they'll land is another matter, and sitting under them is inadvisable.

### It Is More Complicated Than You Think

This is direct from RFC 1925 Truth 8 and is the most frequently violated by those that should know better. Deming's appreciation for a system is the formal variant: systems are networks of interdependence, and they cannot be understood by examining the individual parts. The Unix Philosophy's preference for modularity is a response to this, not a denial of it. You build components precisely because the composed system will be complicated enough on its own without each component adding unnecessary complexity.

Cantrill adds the organizational perspective: systems embed the values of the organizations that build them. If the organization is confused about its values, the system will be confused about its purpose. Confusion compounds across boundaries, seven autonomous organizations each making locally rational decisions will produce a globally incoherent system. This is NOT a failure of the individuals, rather it is a property of systems.

### Problems Don't End

It is always something. This is not pessimism; it is the conditional fact of every complex system. Deming's continuous improvement is predicated on this: there is no state of "done", only a current state and a direction of travel. The Unix Philosophy's "design for change" assumes it. Cantrill's career in debugging is built on it.

The measure of a system, or an organization, is not the absence of problems. It is the speed and quality of response. An organization that punishes problems will stop hearing about them; the problems won't stop.

---

## Part III: Values

Values are choices, unlike principles. They admit tradeoffs. Unlike mission, they are specific enough to guide daily decisions. The values below represent what these four traditions converge on as priorities for systems leadership. Other values are legitimate; these are the ones this framework optimizes for.

### Optimize the System, Not the Parts

Possible Deming's most consequential insight: the performance of a system is not the sum of the performance of its parts. Optimizing parts independently degrades the whole. Ninety-four percent of outcomes are determined by the system; the individuals within it are operating with the systems constraints.

RFC 1925 Truth 5 warns against agglutinating separate problems into a single solution, but the inverse is equally dangerous; fragmenting a system problem into component problems and "solving" each one independently. Truth 6 observes that it is often easier to move a problem around rather than solve it; component-level optimization is often just relocating the problem.

The Unix Philosophy operationalizes this through composability: build the components with clean interfaces so the system can be optimized at the level of relationships between them. Cantrill's values-as-architecture insight explains why this is so hard in practice. If different teams hold different values, they'll optimize their components for different things, and no amount of integration work will make the system coherent after the fact.

This value has a practical corollary: when something isn't working, look at the system first before the people. And when you redesign, factor in the people using the system, design the integration first, and the components will follow.

### Simplicity, Earned Through Mastery

RFC 1925 Truth 12 – perfection is reached NOT when there is nothing left to add, but when there is nothing left to take away. This is the aspiration. The Unix Philosophy's entire mantra is built on it. Deming's "build quality in" instead of "inspect quality out" is the same perspective applied across processes.

Simplicity is not the starting condition, but rather the end. It is earned by thoroughly understanding the problem deeply enough to know what's essential and what's accidental. Cantrill's insistence on rigor – understand before you change, resist the temptation to quick hypotheses – is the discipline required to get there. Premature simplification is just ignorance with good aesthetics.

This means that you have to tolerate complexity while you're learning. It means building prototypes with the expectation that you'll throw them away. It means accepting that the first version will be wrong, and the second version will be less wrong, but the process does not end. This is a limit, not a destination.

### Humans — All of Them — as the Design Center

Deming's psychology pillar – people have intrinsic motivation, which management systems tend to destroy. His point 8: drive out fear, so that everyone may work effectively. The Unix Philosophy values programmer time over machine time, clarity instead of cleverness.

Cantrill sharpens the point into a concrete demand: design for the operator. The person who runs the system, who gets the call at 3am, has to debug a failure across components that were never designed to be debugged together. The forgotten operator, the one the industry said, doesn't need to exist because everything should be in the cloud.

It extends beyond the operators, design for every human the system touches. The end user who didn't choose it, the new team member that must learn it, the auditor that has to verify, the successor that has to maintain. RFC 1925 Truth 4 stands to remind us that some things can only be understood through experience. We must value operational experience as a form of knowledge, and design systems that make experience survivable.

### Theory and Practice as Inseparable

Deming's theory of knowledge, experience without theory teaches nothing. The PDSA cycle requires both prediction and an observation, refined through iterations. RFC 1925 Truth 11 warns that old ideas will be endlessly recycled with new names; without theory there's no way to determine what's been a recycled failure or a recycled success.

The Unix Philosophy bridges this through prototyping. Theory and practice in rapid alternation. Cantrill operationalizes this through observability. You cannot learn from a system you cannot see. If the system is not instrumentable, you cannot close the loop, and you are stuck with opinions.

Observability is therefore not a feature nor a nice-to-have. It is the mechanism by which learning occurs. A system without observability is a system that cannot improve. Its operators cannot distinguish between what they believe and what is true. Invest in observability the way that you invest in the system itself because without it, every other investment is a guess.

### Design for Change

RFC 1925 Truths 7 and 9: it is always something, and you always need more. The only constant is that the system will need to adapt and will need to change. The Unix Philosophy's Rule of Separation is an architectural response: mechanism persists, policy changes, and if you've entangled them then every policy change requires re-engineering the mechanism.

Deming's continuous improvement assumes change is the normal state. Cantrill's co-design philosophy adds a temporal dimension: integration cost is lowest at design time. The more independently the systems evolve, the more expensive it becomes to change them in coordinated ways later. This is not an argument for autonomy. It is an argument for being deliberate about where boundaries are drawn between integrated and autonomous, and for accepting the cost of whichever side you land on.

Designing for change means building systems that can be understood, observed, and modified by people who weren't present when the original choices were made. It means documentation that captures the "why", not just the "what". It means preferring reversible decisions over irreversible ones and investing more care in the irreversible ones.

---

## Part IV: Values as Architecture

This section stands apart from the preceding because it exists at a different level. The principles and values above describe what to optimize for. This section describes the "why organizations fail to do so" and what to do about it.

Every organization embeds within its systems, process, and culture the values it embodies. The result is that different parts of the organization optimize for different things, and the overall system is incoherent. Not because anyone is wrong, but because no one made the tradeoffs explicitly.

Cantrill's taxonomy of platform values - composability, debuggability, operability, performance, security, simplicity, transparency, velocity, and the rest – are all good things. The point is not that some are bad versus good. The point is that they are in tension. You cannot maximize velocity and rigor at the same time. You cannot maximize security and expressiveness. The same goes for simplicity and completeness.

An organization that hasn't decided which values it views as a priority will discover its values through conflict. Teams that value velocity will clash with teams that value rigor. Both will be correct within their perspective, and neither will understand why the other is being unreasonable. The resulting political battles will be held as personal when they're structural.

The corrective action is to make the tradeoffs very explicit. Clearly state which values your organization prioritizes. Clearly state what you're willing to sacrifice, and that which you are not. The part that most organizations skip – hold to those stated values, even when, especially when, they become inconvenient. Cantrill's principles exist to ensure that the values won't be abandoned under pressure.

This is difficult. It is especially difficult in organizations that grew by accretion rather than by design, where autonomous units developed independent cultures and are now being asked to operate as a system. The physics of the situation show that you cannot simply mandate shared values from the center; they must be demonstrated, create the conditions for them to take root, and accept that the process takes longer than anyone wants.

However, the alternative of leaving values implicit and hoping coherence emerges is what produces systems where seven domains each have their own identity structure, their own monitoring approach, their own definition of what a standard is, and their own unique understanding of what the organization values. That is not autonomy. That is the absence of a system.

---

## Part V: Method

How you work is itself a value statement. The method described here synthesizes the four traditions into a practical discipline for understanding and improving complex systems.

**Understand before you change.** Just as you won't and shouldn't debug by randomly changing code, don't debug a system by randomly changing it. This applies to technical and organizational systems. Cantrill's discipline is to iterate between questions and observations. Gather facts that constrain your hypotheses. Don't jump to conclusions and resist the temptation to act before you understand.

**Plan-Do-Study-Act.** Deming's cycle is the method. Plan your changes based on theory, execute the change, study the results. Actually study them, don't just check whether the metric moved. Act on what you've learned, which may mean abandoning the change. The cycle is fast by default. Big, slow cycles are a sign that you're afraid of learning something inconvenient.

**Observe, don't assume.** Above all, a system must be observable. Investment in instrumentation, monitoring, and debugging within the infrastructure pays for itself many times over. Alternatively, if you're making decisions based on opinions rather than data, stop and figure out why the data doesn't exist.

**Fail noisily and early.** Unix's Rule of Repair: when you must fail, fail loudly and as soon as possible. Silent failures compound and a system that hides its problems from its operators is a trap.

**Separate what changes from what persists.** When modifying a system, you need to identify which parts are policy, and therefore easy to change, and which parts are mechanism and should be stable. If you find yourself re-engineering the mechanisms every time policy changes, the boundaries are in the wrong place.

**Don't agglutinate.** When faced with a multitude of problems, resist the urge to solve them all with one single interdependent solution. Solve them separately. The integration cost of separate solutions is usually lower than the maintenance cost of a combined one.

**Match the solution to the context.** One size never fits all. The right answer depends on the constraints, the people, the history, and the values of the organization. A solution that works in one context may be an outright failure in another, not because it's wrong but because it doesn't fit.

---

## Quick Reference

### Principles (Universal Constraints)

| Principle |
|---|
| It Has To Work |
| Hard constraints are real |
| It is more complicated than you think |
| Problems don't end |

### Values (Chosen Priorities)

| Value |
|---|
| Optimize the system, not the parts |
| Simplicity, earned through mastery |
| Humans as the design center |
| Theory and practice are inseparable |
| Design for change |

### Method (How You Execute)

| Method |
|---|
| Understand before you change |
| Observe, don't assume |
| Fail noisily and early |
| Don't agglutinate |
| Match solution to context |

---

*It Has To Work.*

---

*Sources: W. Edwards Deming, System of Profound Knowledge and 14 Points for Management. RFC 1925, "The Twelve Networking Truths" (R. Callon, 1996). The Unix Philosophy per McIlroy, Kernighan, Pike, and Raymond. Bryan Cantrill: "Platform as a Reflection of Values" (2017), "Principles of Technology Leadership" (Monktoberfest 2017), "The Forgotten Operator" (2023), Oxide Computer Company RFD 2: Mission, Principles and Values, and two decades of talks on debugging, observability, and systems software.*
