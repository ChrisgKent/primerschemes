# primerschemes

Central machine readable repo for newly generated PrimerSchemes and PrimalPanels

For a user navigable version please go [here](https://labs.primalscheme.com)


## New formats

### PrimerScheme Versioning

v(w).(x).(y)

`w`: Major Version. (New scheme)
-   `v0`: Refers to autogenerated schemes

`x`: Minor Version. Used to include new alt primers to account for new lineages (Changes to the primers)

`y`: Misc version. Used to include changes to file format or change to primer re-balancing volumes (No primer changes)


### PrimerName Format

```{uuid}_{amplicon_number}_{direction}_{primer_number}```

- ```uuid```: 8 digit uuid linking each primer to the corresponding MSA / scheme

- ```amplicon_number```: The number of the amplicon. 0 indexed int. Not enforced to be continuous

- ```direction```: If the primer is a forward or reverse primer. ```LEFT``` or ```RIGHT```

- ```primer_number```: The number of each primer within each 'primercloud'. 0 indexed int. Not enforced to be continuous


### Directory Format

This is the new format for how schemes will be stored in this repo

```
primerschemes / primerpanels
  ├── README.md
  └── {schemename}
      └── {ampliconsize}
          └── {schemeversion}
              ├── README.md
              ├── info.json
              ├── primer.bed
              ├── reference.fasta
              └── work
                  ├── {msa}.png *
                  ├── {msa}.fasta * 
                  ├── amplicon.bed
                  ├── config.json
                  ├── file.log 
                  └── {misc files} *
```
\* Can have multiple

- ```schemename```: A lower case, only containing [a-z0-9-] and must start/end on a alphanumeric. Use of '--' is reserved for autogenerated schemes ({common-name}--{taxid})

- ```ampliconsize```: The ampliconsize specified when the scheme was created. Actual size is ±10%

- ```schemeversion```: Follows naming in PrimerScheme Versioning


## File Formats

`{msa}.fasta`: The MSA used for scheme generation. 

`primer.bed`: The bedfile that contains the primers in the current version

`amplicon.bed`: The bedfile that contains the amplicons of the current version

`reference.fasta`: The "reference" genomes which the primers are indexed against. Can either be consensus genomes derived from the MSA for a specific genome in the MSA (first genome)

`info.json`:
```json
{
"ampliconsize": "int",
"schemeversion": "str",
"schemename": "str",
"primer_bed_md5": "str",
"reference_fasta_md5": "str",
"status": ["withdrawn", "deprecated", "autogenerated","draft","testing","validated"],
"citations": "list[str]",
"authors": "list[str]",
"algorithmversion": "str",
}	
```

`config.json`: All scheme params dumped from primaldigest

`file.log`: Output log from primaldigest

`{msa}.png`: Figure showing a scheme overview


------------------------------------------------------------------------

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/) 

![](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)
