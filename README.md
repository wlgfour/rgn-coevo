# rgn-coevo
The mostly-complete addition of the ability to process coevolutionary data in Mohammed AlQuraishi's RGN.


# DONE
- Script that uses CCMPred to convert from `a2m` format to compressed raw files `raw.gz`.
    - Example of readong from compressed raw files: `ccmpred_raw.ipynb`.
    - NOTE: When running CCMPred, turn APC correction off. That is done in software and can be seen in `read_raw.ipynb`.
    - The script was run on the CASP12(?) dataset and 99% have `raw.gz` files. On especially long proteins, CCMPred seems to fail.
- Read from Mathematica protein record and convert to a tfrecord.
    - Example and verification seen in `convert_to_tfrecord.ipynb`.
    - NOTE: There is not currently a way to generate the protein record.
    - `read_raw.ipynb` demonstrates reading from a `raw.gz` file and outputs what should be written to the protein record using python.
- Read from tfrecord and input to model.
    - The naive input to the model is described and demonstrated in `stagger_seqs.ipynb`.
    - (1) Configuration options to enable coevolution seem to not be in `Code/config.py`, but I remember needing to put them there.
    - The main alerations to the dataflow of the code can be seen:
        - `net_ops.py: read_protein()`
        - `geomnet_model.py: _dataflow()`
        - `geomnet_model.py: 190`

# TODOs
- (1).
- Make a combined dataset that contains coevolutionary data in. 
- Add coevolutionary options to Mathematica config script.
- Train the model

# NOTES
- Running the model with full raw data would result in `EOM` errors, so it was necessary to preform a frobenius norm on the data, redicing the input size for each protein to be `seq_len^2` rather than `(seq_len^2)(21^2)`.
