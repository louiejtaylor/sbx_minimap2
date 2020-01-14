# sbx_minimap2

This is an extension to the [Sunbeam pipeline](https://github.com/sunbeam-labs/sunbeam) to use the minimap2 aligner *instead of* bwa-mem during the mapping step. **Note that this extension supersedes mapping with bwa-mem if it is installed**

## Installing an extension

Extension install is as simple as passing the extension's URL on GitHub to `sunbeam extend`:

    sunbeam extend https://github.com/louiejtaylor/sbx_minimap2

Installation instructions for older versions of Sunbeam are included at the end of this README.

## Running an extension

To run the extension, simply run Sunbeam as usual, requesting `all_mapping` as the target rule:

    sunbeam run --configfile=sunbeam_config.yml --use-conda all_mapping

The `--use-conda` flag is required to let Snakemake know that you want to use the conda environment(s) included with your extension.

This particular extension does not add a new rule target, but instead supersedes the existing (bwa-mem) mapping rule. The logic for this is contained within the rules file and is as follows:

    ruleorder minimap2_align > align_to_genome

## Anatomy

 - `sbx_minimap2_env.yml` specifies the extension's dependencies
 - `sbx_minimap2.rules` contains the rules (logic/commands run) of the extension

-------
    
## Installing an extension (legacy instructions for sunbeam <3.0)

Installing an extension is as simple as cloning (or moving) your extension directory into the sunbeam/extensions/ folder, installing requirements through Conda, and adding the new options to your existing configuration file: 

    git clone https://github.com/louiejtaylor/sbx_template/ sunbeam/extensions/sbx_
    cat sunbeam/extensions/sbx_template/config.yml >> sunbeam_config.yml

