# sc2calc - SARS-CoV-2 genome coordinate converter

`sc2calc` is a command-line utility to convert genomic coordinates on the
SARS-CoV-2 genome between nucleotide and aa positions.  It takes a nucleotide
mutation and outputs the corresponding amino acid substitution.

I mainly wrote this for my own use, but put it out here in case it is of
use to others.


## Usage

Reads from stdin, writes to stdout.  Aims to DWIM (Do What I Mean), so,
accepts a wide range of inputs:

    ./sc2calc

    12345C               # What does SNP C at 12345 translate to?
    nt:12345C            # Same, being explicit that it's nt
    G12345C              # Same and will error if 12345 is not a G
    12345TA              # What do SNPs TA at 12345 translate to?
    12345:GT>TA          # Same and errors if 12345 is not GT
    12345 GT TA          # Same, VCF style input without label column
    ABC 12345 GT TA      # Same, VCF input with label column

    ins:12345:atg        # Insertion of atg at 12345
    12344 A AACG         # Same, using VCF idiom for insertion
    a12345aacg           # Same, different notation
    nt:a12345aacg        # Same, different notation
    ABC 12344 A AACG     # VCF with label column 1
    ABC 12344 AG AACGG   # Same, extended VCF idiom (G matches right)

    del:12345:3          # Deletion of 3nt at 12345
    del:12345:gtg        # Same and will error if 12345 is not GTG
    12345:3-             # Same
    12344 agtg a         # Same, using VCF idiom

Inverse, translating back from AA to nt:

    S:456                # What nt position (leftmost) is aa 456 on S?
    S:356Y               # What nt mutations give substitution ?>Y at 456?
    S:X356Y              # Same but errors is 456 is not X
    aa:S:X356Y           # Same but explicit about AA

