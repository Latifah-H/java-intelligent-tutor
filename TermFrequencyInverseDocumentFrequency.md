# TF-IDF #
Resources used : [Wikipedia entry for TF-IDF](http://en.wikipedia.org/wiki/Tf%E2%80%93idf)

### Calculating Term frequency ###
  * Each document is converted to CompilationUnitFacade. Thus the mentioned properties of any code can be accessed easily :
    1. ImportDeclarations
    1. MethoInvocations
    1. ClassInstanceCreations
    1. VariableDeclarations
    1. SuperTypes
  * While calculating tf in any general scenario,
` tf for each term = (num of occurrences of that term) / (number of terms in the document). `
  * But we are interested only in the above 5 types of terms. So counts of each of the 5 types of terms are maintained.
  * So in our case, tf for any term = (num of occurrences of that term in its specific type) / (total number of terms for the corresponding type).

### Calculating Inverse Document Frequency ###
  * Number of documents containing each term in the dictionary will be maintained in a persistent manner. Either a db table or a file.
  * Every time new documents are added, the dictionary will be updated with the new words present in the documents that was not present in the dictionary earlier and its document frequency will be updated too.