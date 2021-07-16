# sc2calc - SARS-CoV-2 genome coordinate converter

`sc2calc` is a command-line utility to convert genomic coordinates and
mutations on the SARS-CoV-2 genome between nucleotide and aa positions.

No installation is required, just run `./sc2calc`.  The script accepts
a wide range of notations, see the examples below.


## Usage

The script reads from stdin, writes to stdout.  Here are examples:

    ./sc2calc

    12345C               # What does SNP C at 12345 translate to?
    nt:12345C            # Same, being explicit that it's nt
    G12345C              # Same and will error if 12345 is not a G
    12345TA              # What do SNPs TA at 12345 translate to?
    12345:GT>TA          # Same and errors if 12345 is not GT
    12345 GT TA          # Same, VCF columns 2, 4, 5
    ABC 12345 GT TA      # Same, VCF columns 1, 2, 4, 5

    ins:12345:atg        # Insertion of atg at 12345
    12344 A AACG         # Same, using VCF idiom for insertion
    a12345aacg           # Same, different notation
    nt:a12345aacg        # Same, different notation
    ABC 12344 A AACG     # VCF with label column 1
    ABC 12344 AG AACGG   # Same, extended VCF idiom (end + start)

    del:12345:3          # Deletion of 3nt at 12345
    del:12345:gtg        # Same and will error if 12345 is not GTG
    12345:3-             # Same
    12344 agtg a         # Same, using VCF idiom for deletion

Inverse, translating back from AA to nt:

    S:456                # What nt position (leftmost) is aa 456 on S?
    S:356Y               # What nt mutations give substitution ?>Y at 456?
    S:X356Y              # Same but errors is 456 is not X
    aa:S:X356Y           # Same but explicit about AA


#### Licence

sc2calc - SARS-CoV-2 genomic coordinate converter  
Copyright (C) 2021  Marco van Zwetselaar <io@zwets.it>  

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.

