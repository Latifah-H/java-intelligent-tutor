# Notes while using different APIs used in the project #
  * Programmer Bob "thinks" he might need a certain object from the API. He knows that kind of object exists because he searched for similar phrases and found that such a thing exists in form of a class in the API.
  * **Spiral path (or trap) of API documentation:**For example, Bob wants to find all the lines of code in a program wherein a method on an object was invoked. He assumes, to achieve this, I need to iterate through all the statements of the source code using the API, i.e. Eclipse jdt API. He searches for "how to parse statements using eclipse jdt" and finds that there is a class called _"Statement"_ in the API. On creating an object of class _"Statement"_ he find a multitude of options provided by the class. Then he searched "how to get the type of Statement in eclipse jdt". He found that there are various types of _"ASTNode"_ objects that represent various types of statements like _"ExpressionStatement, "VariableDeclarationStatement"_ ..etc.. But there was no hint to methods. After reading the names and one line description of all the types of statements, he decided that calling methods might be a part of "ExpressionStatement". Now this class was a concrete class unlike the earlier 2 which were only _abstract_ classes. Even _"ExpressionStatement"_ did not refer to anything related to calling a method. The only useful property of the class seemed to be _"getExpression()"_ which returned _"Expression"_. On reading the description carefully he noted that _"ExpressionStatement"_ class is used only to convert an _"Expression"_ to a _"Statement"_. So he went ahead and looked into details of _"Expression"_. This class again was an abstract class, but the description was succinct in noting the several _types_ of _"Expression"_. And finally he found _"MethodInvocation"_ as a type of _"Expression"_. So now he can deduce the path of searching a method call from a given statements.
_Statement_ --> (**.getNodeType()**) --> _ExpressionStatement_ --> (**.getExpression()**) --> _Expression_ --> (**.getNodeType()**) --> _MethodInvocation_

  * **Simpler path of following an example :**Even after all the research he knew how to convert a type _Statement_ into a _MethodInvocation_. But the basic question was how to obtain the _Statement_ s from actual source code. How to parse the actual thing? On searching he found another bunch of classes like _"ASTParser"_. Unlike most classes, to create an _ASTParser_  he had to call a static method _"ASTParser.newParser()"_ with a some parameter, instead of calling a constructor. On searching again about how to create parser in eclipse jdt he was referred to an example which passed in _AST.JLS3_. Without thinking he passed the same too. The example also mentioned other common settings required to set a new _"ASTParser"_. The example mentioned setting _KIND_ of the parser by _setKind_ . Since Bob had earlier discovered a class called _Statement_ he chose the option _K\_STATEMENT_ for _setKind_.

The example :
_> ASTParser parser = ASTParser.newParser(AST.JLS3);_<br />
> parser.setKind(ASTParser.K\_COMPILATION\_UNIT); <br />
> parser.setSource(unit); // set source <br />
> parser.setResolveBindings(true); // we need bindings later on <br />
> return (CompilationUnit) parser.createAST(null); // parse  <br />


Although this example did not explain the exact way to get _Statement_ s it at least led to a path much easier to follow than the earlier case wherein Bob was travelling in a spiral path.
# Other References #

## Obstacles in learning API ##
_[What Makes APIs Hard to Learn? Answers from Developers](http://doi.ieeecomputersociety.org/10.1109/MS.2009.193)_

50/74 people face problems related to resources for learning API
Out of these :
**40% do not find adequate examples**
28% problems with documentation
**18% No reference on how to use the API to accomplish a specific task**

Notes about examples:
  * Examples help understand purpose of library, usage protocol and usage context.
  * 3 types of code examples:
    1. **Snippets:** Few lines of code intended to demonstrate how to access the API. **Inadequacy**:  Cannot help in putting things together.
    1. **Tutorials:** multiple code segments forming a more or less complete application
    1. **Applications:** code segments from complex applications that can be downloaded from open source repositories.
  * **Users progressively move** from _snippets_ to _applications_ to support their needs.
  * People need examples for:
    1. learning best practices
    1. design of code that uses the API
    1. rationale about API's design

## Problems in Teaching Java ##
_[The ACM Java Task Force Rationale](http://jtf.acm.org/rationale/rationale.pdf)_
  * Although the language itself is simple to teach, the large number of APIs provided results in conceptual overload for students and teachers alike. With newer releases of Java, this problem is unlikely to be resolved due to newer additions of APIs.
  * The ACM task force decided a subset of APIs that are fit for Introductory class to programming by choosing a few APIs that would support different pedagogical strategies.
  * Other findings in the paper concentrate more on specific language or API issues, for eg. static, Wrapper, complexity of Graphics model and GUI.

## Considering Cognitive Traits and Learning Styles ##
_[Considering Cognitive Traits and Learning Styles to Open Web-Based Learning to a Larger Student Community](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.112.1762)_
  * Adaptive course fits to individual characteristics of learners and make learning easier. Creating these courses consists of 2 steps:
    1. Individual needs of the learner need to be detected
    1. Courses have to be adapted according to these findings.