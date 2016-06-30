# CCDB-CSE532-Proj1-
In this project, you will be designing and implementing part of a database for keeping information about clients of a credit card company.  
You will be using the Datalog language supported by the `Flora-2` system ([http://flora.sourceforge.net]). The lecture slides provide a brief introduction to the use of Flora-2. You are not required to
build any GUI or store any data in a DBMS (we do not have the time to discuss those aspects of Flora-2). Instead, you should keep all data, rules, and queries in one file. When the file is loaded,  
myprompt> ..../flora2/runflora  
flora2 ?- [myproj1].  

all queries are to be run as part of this loading and all answers to the queries are to be printed out like this (or similar):  
---- Query 1 -----  
answer1  
answer2  
...  
---- Query 2 ----  
answer1  
answer2  
...  
etc.  

##1 General Description
CCDB contains information about clients (people, organizations), their credit card accounts, owners and authorized users of the cards, credit limits, and current balance. For simplicity, we do not include transaction histories and other stuff. A card owner can be a person (with the usual attributes like name, date of birth, etc.) or an organization (again, with the usual attributes like name, address, etc.). An authorized user is always a person.  

##2 Required Data  
The data items required by your system roughly fall into these categories:  
* Information about clients like the id, name or an organization or a person, date of birth (if a person), address, person with signature authority (organizations only; several people can have signature authority in an organization).
* Profile information about credit card accounts like account number, the owner, other authorized users. If the owner is an organization then the person with the signature authority is also an authorized user of the card. A credit card must have exactly one owner, but it can have zero or more (other) authorized users.  
* Financial information about accounts, including the current balance, credit limit. Note that the data model underlying Datalog is essentially relational, so the design of the relations for Project 1 should follow the best practices of relational database design.1 The structure of the above information is such that naive ways of organizing the data in relations will cause violation of 4NF (Fourth Normal Form). So, you should normalize the schema.  

1. Make my changes
  1. Fix bug
  2. Improve formatting
    * Make the headings bigger
2. Push my commits to GitHub
3. Open a pull request
  * Describe my changes
  * Mention all the members of my team
    * Ask for feedback
##3 Queries
You are to implement the following queries. You do not need to use function symbols or lists, but for some queries you would need to use negation (\naf), aggregate operators (e.g., avg{... | ...}), quantifiers (forall(...)^... and exist(...)^...), and recursion. You might also need to use some builtins like =, ! =, \is, etc.  
1. Find all pairs of the form (user,signer), where user is an authorized user of an organization’s
credit card, signer is a person at that organization with signature authority, and the balance
on the card is within $1,000 of the credit limit. For each user/signer, show Id and Name (see
the expected output for an example).  
1. Find all users (Id, Name) who own four or more cards and are authorized non-owner users for
three or more other cards. This query must use aggregates.  
1. Find the credit cards (acct. numbers) all of whose signers (i.e., people with signature authority
of the organizations that own those cards) also own personal credit cards with credit limits at
least $25,000. This query must use quantifiers.  
1. Find all pairs (U,C) where U is an indirect user of the credit card C. (For each user, show Id and
Name. For credit cards, show the account number.)
A user U is an indirect user of a credit card C if either  
  * U is a direct user, i.e., U is one of the authorized users of C ; or
  * U is a direct user of a credit card C2 and the owner of C2 is an indirect user of C.
1. Find the total of all balances for the credit cards that have Joe as one of the indirect users. This
query can (and should) reuse some of the earlier queries.
