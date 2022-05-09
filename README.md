# AnaLog
#### Dataset Notation

**Operator** The main logical connective in the premise (P). Such operators include:

  Conjunction (AND), Disjunction (OR), Conditionals (CON), Universal Quantification (UNI). 

**Premise**  A premise.

**Hypothesis** A hypothesis.

**OpSpec** Specific information about the type logical operator:

_AND/OR_

    S: conjunction/disjunction between sentences (e.g. P: James is arriving later than Elizabeth **and/or** James is arriving earlier than Patricia.)
    
    NP: conjunction/disjunction between noun phrases (e.g. P: James is arriving later than Elizabeth **and/or** Patricia.)
    
    VP: conjunction/disjunction between verb phrase (e.g. P: Jennifer is to the north of Elizabeth **and/or** is to the east of Patricia.)

_CON_

    ONLYIF: the main logical operator is of the lexical form 'only if' (e.g. P: Elizabeth is arriving earlier than James **only if** Michael is stronger than Barbara.)    
    
    UNLESS_PREFIX: the main logical operator includes 'unless' at the beginning of the premise (e.g. P: **Unless** Linda is behind Barbara, Elizabeth is to the west of Mary.)   
    
    UNLESS_INFIX: the main logical operator includes 'unless' within the premise (e.g. P: Elizabeth is to the left of David **unless** Michael is in front of Barbara.)
    
    IFTHEN: the main logical operator is of the lexical form 'if ... then ...' (e.g. P: **If** Elizabeth is older than Jennifer **then** Linda is smaller than Jennifer.)      
    
    IF: the main logical operator is of the lexical form ' ... if ... ' (e.g. P: William is smaller than Patricia **if** Linda is older than Robert.)               
  
_UNI_

    EACH: the main universal quanitifer is represeneted by the lexical item 'each' (e.g. P: **Each** director is to the west of Patricia. John is a director.)
    
    EVERY: the main universal quanitifer is represeneted by the lexical item 'every' (e.g. P: **Every** director is to the west of Patricia. John is a director.)


**SentType** The type of hypothesis:

O-E: Overlap Entailment

O-NE: Overlap Non-Entailment

NO-E: No Overlap Entailment

NO-NE: No Overlap Non-Entailment

**SentCat** The category of the sentence, determined by the analytic reasoning predicate. We use SR to denote spatial reasoning, and CR to denote comprative reasoning. 

**RP_1** The first analytic reasoning phrase in the premise. We code the phrases according to the following notation:
 
                 
                'is to the left of':'LR',
                
                'is to the right of':'LR',
                
                'is in front of':'FB',
                
                'is behind':'FB',
                
                'is above':'AB',
                
                'is below':'AB',
                
                'is to the north of':'NS',
                
                'is to the south of':'NS',
                
                'is to the east of':'EW',
                
                'is to the west of':'EW',
                
                'is larger than':'LS',
                
                'is smaller than':'LS',
                
                'is faster than':'FS',
                
                'is slower than':'FS',
                
                'is arriving earlier than':'EL',
                
                'is arriving later than':'EL',
                
                'is stronger than':'SW',
                
                'is weaker than':'SW',
                
                'is younger than': 'YO',
                
                'is older than':'YO'.
                
**RP_2** The second analytic reasoning phrase in the premise. Can remain empty if the premise only includes one anaytic reasoning phrase.

**Spans** Character positions of the named-entities in the premise. Computed and formatted according to the LUKE tokenizer.

**OpLexicalSpecs** Any additional information needed (beyond **OpSpec**), such as lexical items and subsequence sentences that are randomized (using a normal distrburtion) and should be kept track: 
  
  _AND/OR_
  
  The conjuncts of AND (S, NP, VP) and disjuncts of OR (S, NP, VP) are randomized. We use **LM** to denote parsing entities to the left of the premise's logical operator are required to make a valid logical deduction (e.g. P: Patricia is right of James and Elizabeth --> O-E: Patricia is right of James), while RM is used denote parsing entities to the right most part of a opereator are required to make a valid logical deduction (e.g.  P: Patricia is right of James and Elizabeth --> O-E: Patricia is right of Elizabeth).
  
  _CON_
  
  We randomly sample from the following lexical _[if, when, even though]_ to represent the main logical operator within **CON IF** sentences.
  
  _UNI_
  
  We randomly sample from the following list of NPs: _director, model, soldier, participant_.
  

**GoldLabel** The prediction a language model should make when solving this AnaLog. As this is a binary task, we code '1' to denote entailment and '0' to denote non-entailment.

**Grammaticality** As only half of the O-NE hypotheses are grammatical, we keep track of the grammaticality of all premise - hypotheses pairs:

UG: ungrammatical

G: grammatical



----

#### BERT + SVM & Logistic Regression 
Run pipeline on the entire dataset: \
`python src/bert_pipeline.py --datadir data --outdir out
`

Run pipeline on a subset of the dataset (e.g. for debugging purposes): \
`python src/bert_pipeline.py --datadir data --outdir out --nitems 100
`

Set the maximum number of iterations for the Logistic Regression optimiser in case it fails with only a few data points:\
`python src/bert_pipeline.py --datadir data --outdir out --nitems 20 --lr_maxiter 500
`
