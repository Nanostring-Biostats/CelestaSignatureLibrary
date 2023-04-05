## Overview

This repo contains a library of signature matrices and tuning parameters for the CELESTA cell typing method. The files are in .csv format and can be uploaded as input to the CELESTA cell typing module in AtoMx. You can download your desired csv files by navigating to the file, clicking "Raw", and then saving as a .csv file.  

## CELESTA 

The CELESTA algorithm performs cell typing by taking into account each cell's marker expression profile and, if necessary, spatial information. Cell typing calls are guided by a signature matrix which specifies the marker(s) known to have high/low expression for each cell type. When the probability is sufficiently high, a cell is considered an "anchor cell". When the probability is not sufficiently high to make a high certainty cell type call, the algorithm also considers spatial information by taking into account the cell type calls of neighboring cells. These are considered "index cells". The probability thresholds can be tuned by updating the tuning parameter input file to increase (or decrease) the number of a given cell type by decreasing (or increasing) the high_expression_threshold_anchor or high_expression_threshold_index for anchor and index cells respectively.

## Signature matrix format

The signature matrix defines which protein(s) will be used as markers for which cell types.

1 (0) indicates the protein should (not) be expressed in the celltype. NA indicates the protein is not considered in the scoring function.

Lineage_level indicates `clusteringlevel` _ `celltype number descended from` _ `overall consecutive celltype`

For example, in the default human signature matrix, the lineage "2_1_6" for "tcell" indicates that it is in the 2nd stage of cell typing, descended from the overall cell type 1 ("immune"), and the 6th cell type overall.

## Tuning parameters format

The low expression threshold default values in general are robust, and thus we recommend tuning only the high expression threshold values, 1-2 markers at a time as necessary. Descriptions for the parameters are as follows:
* `high_expression_threshold_anchor`: if a cell’s probability for this marker being highly expressed is greater than this threshold, the cell can become an “anchor” cell.
* `high_expression_threshold_index`: the cell's probability for this marker being highly expressed must be greater than this baseline threshold to be assigned to the cell type.
* `low_expression_threshold_index` , `low_expression_threshold_anchor`: for markers in the signature matrix that are not supposed to be expressed for the celltype (0), the marker expression probability needs to be less than this value. The default being 0.9/1 implies this is not a strict threshold by default. i.e., we may consider a cell as an immune cell, as long as the non-CD45 marker scores are < 0.9/1.
