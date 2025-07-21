# To-Do List


!!! note "! P1"

    - [ ] ELECTRA
        - [ ] GANs for text challenges
        - [ ] generator-discriminator size, weight tying, 
        - [ ] variants of electra
        - [ ] generator as adverserial using RL
    - [x] CodeBERT
        - [x] MLM + RTD : bimodal PL-NL, RTD: unimodal PL/NL
        - [x] NL code search, code documentation generation, NL-PL probing
        - [x] PL, NL generator - n-gram with bi-directional context
        - [x] 1 NL code search - MRR - fine tuned 
        - [x] 2 NL-PL probing - accuracy - fine tune but codebert freezed
        - [x] 3 Code doc gen - smoothed BLEU - use codebert as encoder, train decoder
        - [x] 4 generalizing to PL not in pre-training - smoothed BLEU - fine tuned
        - [x] Late fusion for code search

!!! note "!! P2"
    - [ ] BLEU score
    - [x] MRR
    - [ ] ~~What is AST (abstract syntax tree)~~