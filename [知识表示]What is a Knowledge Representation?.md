# What is a Knowledge Representation?
# 什么是知识表示？  
Perhaps the most fundamental question about the concept of knowledge representation is, What is it? We believe that the answer is best
understood in terms of the five fundamental roles that it plays.  
对于知识表示的概念来说，最为基本的问题是——知识表示是什么？我们认为通过了解知识表示的五个基本特点，才能更好地理解知识表示。  
# Role I: A KR is a Surrogate
# 知识表示是一种surrogate  
Any intelligent entity that wishes to reason about its world encounters an
important, inescapable fact: reasoning is a
process that goes on internally,
while most things it wishes to reason about exist only externally. A program
(or person) engaged in planning the assembly of a bicycle, for instance, may
have to reason about entities like wheels,
chains, sprockets, handle bars,
etc., yet such things exist only in the external world.  
任何一种希望对其所在的世界进行推理的智能体，都必定遇到这样一个重要又无法摆脱的事实——推理是在内部进行的过程，而推理的对象往往只存在于外部。
比如在一个程序（或者一个人）试图拼装一台自行车时，可能需要在像车轮、链条之类的实体上进行推理，而这些实体只会存在于外部世界。  
This unavoidable dichotomy is a fundamental rationale and role for a
representation: it functions as a surrogate
inside the reasoner, a stand-in
for the things that exist in the world. Operations on and with
representations substitute
for operations on the real thing, i.e., substitute
for direct interaction with the world. In this view reasoning itself is in
part a surrogate for action in the world, when we can not or do not (yet) want
to take that action.    
这种无法避免的对立（内部和外部）是表示的基本原理和作用。这种对立，在推理者内部作为一个surrogate，一个世界中的实际事物的替身而发挥作用。
在表示上进行操作，以及利用表示进行操作，替代了在实际的事物上进行操作。也就是说，替代了和现实世界的直接交互。
在这种观点下，推理本身就是现实世界的中某种行为的surrogate的一部分，这种行为是我们在推理时还不能做到或者（尚且）不希望做到的。  
Viewing representations as surrogates leads naturally to two important
questions. The first question about any
surrogate is its intended identity:
what is it a surrogate for? There must be some form of correspondence
specified between the surrogate and its intended referent in the world; the
correspondence is the semantics for the
representation.    
如果我们把表示看做surrogate，这就自然会导致两个重要的问题。第一个问题是这个surrogate希望指向的身份：它到底替代了什么？
在这个surrogate和它的存在于现实世界的指向物之间，必然存在某种形式的一致性。这种一致性，就是这个特定表示的语义。  
The second question is fidelity: how close is the surrogate to the real thing?
What attributes of the original does it
capture and make explicit, and which
does it omit? Perfect fidelity is in general impossible, both in practice and
in principle. It is impossible in principle because any thing other than the
thing itself is necessarily different from the
thing itself (in location if
nothing else). Put the other way around, the only completely accurate
representation of an
object is the object itself. All other representations
are inaccurate; they inevitably contain simplifying assumptions
and possibly
artifacts.  
第二个问题是精准度：这个surrogate和实际的事物到底差距多大？有哪些原事物的属性被这个surrogate保留了（并且使其表示更明确了），又有哪些被忽略了？
完全精准一般情况下是不可能的。既在实践上不可能，也在理论上不可能。
说完全精准在理论上不可能，是因为任何除物体本身之外的其他物体，都必然与这个物体有所不同。（至少存在的位置不一样）
换一种说法，唯一存在的对于某一物体的精确表示只有物体本身。其他任何的表示都是不精确的，那些表示不可避免的包含了一些含有简化事物的假设，
可能还有人为附加的成分。  
Two minor elaborations extend this view of representations as surrogates.
First, it appears to serve equally well for
intangible objects as it does for
tangible objects like gear wheels: Representations function as surrogates for
abstract
notions like actions, processes, beliefs, causality, categories,
etc., allowing them to be described inside an entity so it
can reason about
them. Second, formal objects can of course exist inside the machine with
perfect fidelity:
Mathematical entities, for example, can be captured exactly,
precisely because they are formal objects. Since almost
any reasoning task
will encounter the need to deal with natural objects (i.e., those encountered
in the real world) as
well as formal objects, imperfect surrogates are
pragmatically inevitable.  
两个小的解释延伸出了这种把表示看做surrogate的观点。第一个是，这种方法可以同样很好地处理无形的物体，就像处理齿轮那种有形的物体那样。
一些对于抽象概念的surrogate，比如行为、过程，其表示仍然允许其在一个实体内部被描述出来，故可以用来被推理使用。
第二个是，形式化的事物自然可以无损地存在于机器内部，比如数学上的实体，作为形式化的事物，可以精准地被描述出来。
由于几乎所有推理任务都要面对像处理形式化事物那样处理自然事物（比如那些现实世界中的推理）的需求，从实用的角度说，不完美的替代是不可避免的。
