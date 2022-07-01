# BasketAnalysis
Learning principles and concepts of Association Analysis.

## Introduction and Terms

### What is it about?

> Association Analysis is about setting up association rules, i.e., predicting patterns of connections between attributes. If one event A together with event B happened, can we expect to see those two happening again? If n attributes are known, can we determine m attributes unknown. It all comes clear with examples, so don't worry!

### Important terms

- Association: connection between events.
- Events: attributes known from a datapoint.
- Item: one attribute observed.
- Itemset: vector of items. One would refer to them as k-Itemset, with k in naturals. Described as I.
- Association Rules: pattern describing connection between events. Assumption of a relation between items. RS: LS (Right Hand Side: Left Hand Side) to notate rules.
    - LS, RS are contained inside I. And their intersection is empty.
- Transaction: an individual, an entity, a datapoint, a group of items or attributes. Ex.: 1 purchase, 1 customer.
    - Vector of boleans with attributes or fields being the items. Some pre-processing may need to come in hand for the table.

### Limitations of Association Analysis

- Rules inhereted from the data are no use for the pattern mining.
- Not all rules are interested.
- Rules might be nonsencial. Ex.: You get out your car and the sun is shining.

### Applications of Association Analysis

- Stock Market: if Apple was purchased by some buyer, what other stocks can be expected?
- Genetics: genes or attributes in DNA would mean what others?
- **Basket Analysis**: given these item purchases your basket, what do the patterns observed dictate that you will buy / add to your basket up next?

## Let's start with the math now

Now that the introduction and some definitions were presented. Let's see how we can apply the concepts into doing some calculations.

### Frequent Patterns

> Frequent patterns are relationships between attributes or items that appear often in the dataset. Usually they gather more interest for Data Analysis.

### Absolute and Relative Support

The first is simply the count of an item or an itemset. 

The second (by the way the important one) is this absolute count that you learned above, divided by the total of instances or datapoints from the dataset.
It could be also be thought as the probability of seeing this specific item or itemset in the transaction dataset.

- It can be of either an item, reflecting the percentage of ocurrence.
    - Denoted as Support(X) = P(X).
- Or of a rule, reflecting the joint percentage of all items in that rule.
    - Denoted as Support(X->Y) = P(X U Y) Union here.
> Ultimately, it reflects the relevance of an itemset. And one should set a threhold for minimum support to indicate relevance.

### Confidence

Confidence is the support of a rule compared to the support of the left hand side. Bringing to our Basket Analysis example, it could be the calculation of the frequency (or support) of Beers and Sweets, divided to the frequency of Beers.

> If one k-itemset apparently cause the entity to have (k-itemset U n-itemset), what is the calculation of this second itemset frequency in the population of the transactions that have the k-itemset?

## How do we mine these rules?

### A-priori algorithm

1. Generate rules. Done by combinatorial calculations. Ex.: 4-itemset. You choose, for instance, 1 item to be on the left-hand side and the other three are on the right-hand side, this results in 4 possibilities (4 1). One would have to add this possibilities to (4 3) and (4 2), resulting in 14 possible rules. (4 4) is not in because it would be leaving either LS or RS empties.
    
    a. The number of generated rules is 2^k - 2. This only takes in account the possibilities of choosing the specific smaller itemsets within a 4-itemset.
    
    b. If we expand the sub itemsets within the 4 one and calculate the rules generated for each, we would get 50 rules in total. (4 1)*((3 1)+(3 2)+(3 3)) + (4 2)*((2 2)+(2 1)) + (4 3) = 50.
    
2. Identify important rules
    
    a. Find frequent itemsets, starting with more items and fewer combinations to less items and more combinations. The itemsets have to meet a certain minimum support (sigma).
    
    b. Generate rules only for these itemsets.
    
    c. The rules have to meet a mininum confidence (gamma) to be considered strong.
    
    d. Go to next iteration for the itemsets with the valid rules > threshold for minimum confidence and support.

### Lift

Lift is supplementary significance measure. It basically tells us how much better the rule predicts the RS than we would expect anyhow.

- It is calculated as the confidence of the rule divided by the support of the RS. (Lift X->Y).
- Lift = 1: No correlation between premise and conclusion.
- Lift > 1: Positive correlation.
- Lift < 1: Negative correlation.

## In the real world

### Different types of associations can be mined

- Boolean Association: presence or absence of values.
- Quantitative association: Ex.: Age being a certain value and the the Credit Risk being another.
- Single and multi-dimensional association: varying the k of the k-itemsets and the number of items in the LS and RS. 
- Association on different level of abstractions: Ex.: Generic names such as food product or the specific food.

1. The retailers' lines of products are measured by 10s and 100s thousands.

2. A-priori would need to create a big size of itemsets and the rules of each one. It does not work well with common DBMS approaches.
    
    a. FP-Growth as alternative without candidate generation.





















