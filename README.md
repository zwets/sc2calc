# sc2calc - SARS-CoV-2 genome coordinate converter

`sc2calc` is a small command-line utility to convert genomic coordinates
on the SARS-CoV-2 genome between nucleotide and aa positions.  It takes a
nucleotide position or mutation and outputs the corresponding amino acid
position/substitution, and vice versa.

I mainly wrote this for my own use, but it might be helpful for others.


## Usage

The idea is that `sc2calc` is maximally DWIM (Do What I Mean), accepting


    sc2calc [INPUT]

Reads from stdin, writes to stdout.  Accepts the following inputs:

    12345                # What aa does nt position 12345 correspond to?

    12345G               # What does SNP ?>G at 12345 translate to?

    T12345G              # Same and will error if 12345 is not a T

    12345:T>G            # Same, different notation

    12345 T G            # Same, VCF input without column 1

    ABC 12345 T G        # Same, VCF input with column 1

    ABC 12345 TACG T     # Same, using VCF idiom for deletion ACG

    del:12345:3          # Deletion of 3nt at 12345

    del:12345:atg        # Same and will error if 12345 is not ATG

    ins:12345:atg        # Insertion of atg at 12345

Inverse, translating back from AA to nt:

    S:456                # What nt position (leftmost) is aa 456 on S?

    S:356Y               # What nt mutation is substitution ?>Y at 456?

    S:X356Y              # Same but errors is 456 is not X

## Output

Output is tab-separated, having the same columns as the input, followed
by:




