# Evaluator
An agency provides background check service. Given a candidate they can verify
various things: credit, criminal records, employment verification, citizenship check,
etc. There may be more things they can verify in the future.

To make things easy we will use social security number to represent a candidate.

Design a class library with the following:

A candidate can be represented using the social security number, first name, and last name.

Provide facility to evaluate a candidate based on various criteria selected.

The result of evaluation is either an approve or a disapprove. If it was a 
disapprove, the reason(s) are provided. The result of evaluation should be
candidate's full name, their social security number, and the result of the evaluation
(along with details as necessary).

Design the library so that a user of the library can decide which criteria to
use for evaluation. They can select one or more criteria. They can also provide their
own criteria beyond what the library provides.

For each of the criteria (for example to check criminal records) we will pretend
that such code can be implemented by talking to a database or a web service.
For the purpose of this exercise we will generate a random response in the code
for the analysis of a criteria like criminal record.
