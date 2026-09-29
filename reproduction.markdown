---
title: Reproducing
---

This page contains instructions for reproducing the results of the paper including:
* Generation of plots and tables used in the paper
* Re-running the experiments to generate the results in the paper

# Technical Setup

## VaRA-Tool-Suite
We use the [VaRA Tool-Suite](https://github.com/se-sic/VaRA-Tool-Suite) (VaRA-TS) for our experiments.
Our experiments are implemented on a [separate branch](https://github.com/se-sic/VaRA-Tool-Suite/tree/dev-HiddenConfig) (`dev-HiddenConfig`).
Please follow the instructions in the [documentation](https://vara.readthedocs.io/en/vara-dev/vara-ts/vara-buildsetup.html) to set up a local copy of the VaRA Tool-Suite and install all dependencies.
Once installed, follow the [post-install steps](https://vara.readthedocs.io/en/vara-dev/tutorials/getting_started.html#post-install-steps) to set up the VaRA-TS environment.

## Benchbuild
The VaRA-TS uses [benchbuild](https://github.com/PolyJIT/benchbuild) as an underlying experiment framework.
For this paper, we implemented some quality of life improvements that we maintain on an individual [fork](https://github.com/LuAbelt/benchbuild/tree/dev-VaRA).
Please make sure to use this benchbuild for full compatibility.

## AST Pattern Matching Tool
We provide the implementation of our AST matching tool on [GitHub](https://github.com/se-sic/HVar-Detector).

# Preparing the VaRA-TS Environment
In order to setup the correct case studies and revisions unpack the `results.zip` file into your `$VARATS_ROOT` directory (The directory in which you setup the VaRA-TS).

The `results.zip` file contains all case-studies, as well as all results produced in our measurement environment.

# Reproducing Plots and Tables
With the provided results, the VaRA-TS can be used to re-generate most tables and plots used in the paper, along as additional variations.
*Note*: Some manual styling and formatting may be added after generation to match the style of the paper.

The VaRA-TS provides a set of commands to generate plots and tables with individual options.
For plots and tables as used in the paper and supplement, we provide a shorthand definition of artefacts that can be used to generate the plots and tables with exactly the same options as used in the paper.
For completeness, we also provide a documentation of the individual options for each plot and table.

## Generating using `vara-art`

The VaRA-TS provides the `vara-art` command to generate plots and tables with a single command.
To generate a specific artefact with the same options as used in the paper, and on this website, run the following command in the VaRA-TS environment:
```bash
vara-art generate <artefact>
```

Where `<artefact>` is the name of the artefact to generate.
The resulting 
When the `results.zip` file is unpacked into the `$VARATS_ROOT` directory, the following artefacts are available to generate the plots and tables used in the paper:

- `zmq_benchmark_plot` - Generates Figure 1 of the paper.
- `project_overview_table` - Generates Table 2 of the paper.
- `results_rq1_table` - Generates the result table used in Table 4 of the paper.
- `results_rq1_plot` - Generates the result plot used in Table 4 of the paper.
- `results_rq2_table` - Generates Table 5 of the paper.
- `results_cadical_rq22_plot` - Generates Figure 5 of the paper.
- `discussion_share_plot` - Generates Figure 6 of the paper.
- `setting_mappings_table` - Generates the tables mapping execution setting IDs to specific workload, metric and configuration combination used in the Execution Settings sub-page.
- `conf_alt_mappings` - Generates the tables mapping configuration IDs to specific configuration used in the "Configuration Alternatives" sub-page
- `rq1_all_plot` - Generates a version of the plot in Table 4 including all subject systems.
- `rq21_all_plots` - Generates the full plots for each case study for the visualization of RQ2.1 (Used on the "Additional Plots" sub-page).
- `rq22_all_plots` - Generates the full plots for each case study for the visualization of RQ2.2 (Used on the "Additional Plots" sub-page).

## Generating Plots manually using `vara-plot`
Generally, to generate a plot, use the following command:
```bash
vara-plot <COMMON_PLOT_ARGS> <plot_name> <PLOT_SPECIFIC_ARGS>
```

All plots share some common options to control e.g. the output type and resolution of the plot generated.
You can inspect them using `vara-plot --help`.
In the following, we will discuss only the plot specific options.

The following values for `<plot_name>` are relevant for this paper:
- `libzmq-benchmark`
- `hc-perf-change-summary`
- `hc-setting-kw`
- `hc_significant_alts_share`

The following sections will discuss the use of these plots and which plot specific options they offer (if any)

### `libzmq-benchmark`
This plot represents the benchmark visualized in Figure 1 of the paper.
It does not have any plot-specific arguments.

### `hc-perf-change-summary`
This plot is used alongside Table 4 in the paper to visualize the results of RQ1.
It supports the following plot-specific options:
- `--case-studies` - A comma-separated list of case-studies to include in the plot. Can be any of:
  - `DunePerfRegression_0`
  - `libzmq_0`
  - `libvpx_0`
  - `x264_0`
  - `7zip_0`
  - `brotli_0`
  - `bzip2_0`
  - `ect_0`
  - `gzip_0`
  - `lepton_0`
  - `lrzip_0`
  - `xz_0`
  - `duckdb_0`
  - `mariadb_0`
  - `postgres_0`
  - `HyTeg_0`
  - `FastDownward_0`
  - `cadical_0`
  - `cryptominisat_0`

### `hc-setting-kw`
This plot can be used to visualize the ranges of performance changes with settings or configuration alternatives (RQ2.1 and RQ2.2)
It supports the following plot-specific options:
- `--study` - A comma separated list of case studies to include. See above for supported options. Will generate a separate plot file for each case study.
- `--group-by` - Comma-separated list of columns to group the data by. Use:
    - `setting_id` - For a grouping by execution setting (RQ2.1)
    - `config_alt_id` - For a grouping by configuration alternatives (RQ2.2)
- `--color` - Color to use for plotting
- `--limit-groups` - Limit the number of groups to display. Will try to pick equidistant groups sorted by the range of performance changes.
- `--xlabel` - X-Axis label to use

### `hc_significant_alts_share`
This plot is used in Figure 6 in the paper.
It supports the following plot-specific arguments:
- `case-studies` - Comma-separated list of case studies to include. See above for possible values.
- `metrics` - Comma-separated list of metrics to include. Metrics can be case study specific.
- `workloads` - Comma-separated list of workloads to consider. Workloads are case study specific.

## Generating Tables manually using `vara-table`
The interface for tables is very similar to the ones for plots:

```bash
vara-table <COMMON_TABLE_ARGS> <table_name> <TABLE_SPECIFIC_ARGS>
```

The common table arguments can be queried with `vara-table --help`. Our tables are optimized for `--table-format=LATEX`. None of our tables use table specific arguments.

The following values for `<table_name>` are relevant for this paper:
- `hv_project_overview` - Generates Table 2 of the paper.
- `hc_perf_summary` - Generates the result table used in Table 4 of the paper.
- `hc_perf_sensitivity` - Generates Table 5 of the paper.
- `hc_setting_id_mappings` - Command used by the artefact `setting_mappings_table`.
- `hc_config_alt_id_mappings` - Command used by the artefact `conf_alt_mappings`.

# Reproducing Experiment Data

The VaRA-TS provides a set of commands to run isolated experiments related to the paper.
We will provide a best-effort description of how one can run these experiments on their own hardware.
However, there are some caveats that might require manual intervention or adaption of configuration files.
While we try to list them all here, it is possible that some are overlooked.
The first author is happy to respond to any potential issues that arise while trying to re-run the experiments.

## Setting up containers
Some of our experiments support building and measuring in a `podman` container to ensure all dependencies are available.
Please follow the [container guide](https://vara.readthedocs.io/en/vara-dev/tutorials/container_guide.html), using the base image `DEBIAN_12`, of the VaRA-TS to properly setup the environment.
The experiments for the following case studies were executed in a container:
- `cadical`
- `cryptominisat`
-  libzmq`
- `libvpx`
- `lrzip`
- `xz`
- `duckdb`
- `postgresql`

## Setting up Configuration Alternatives
To include configuration alternatives in the experiments, the VaRA-TS requires that the respective case studies have alternatives defined.
Adding configuration alternatives requires the following components:
1. A patch definition file that is applied to the case study before compilation.
2. Iff the patch uses placeholders for configuration values, a list of alternative values to setup in the patch.

### Adding Patch Definitions
Patches for a project need to be added to the `vara-project-patches` [repository](https://github.com/se-sic/vara-project-patches/).
With some local modifications in the VaRA-TS source one can also only work on a new local branch that exists solely in `$VARATS_ROOT/benchbuild/tmp/patch-configurations`.
A detailed description how to set this up is beyond scope for this document, but the first author is happy to provide guidance on this.

A patch usually consists of a `<patch>.info` file that describes the patch (and optionally, its' arguments) and a corresponding `<patch>.patch` file that contains the actual patch to apply.
The format of the patch file is the same as for the `git apply` command.

### Adding Configuration Alternatives
To setup different values for placeholders to be used in a patch, these alternatives need to be defined in the `.case-study` file of the respective case study.
To the end of the `.case-study` file, add a new section with the following format:

```
---
config_type: PatchVariationConfiguration
0: '{<patch_name>: {<arg_name>: [<arg_value_1>, <arg_value_2>, ...]}}'
...
<n>: '{}'
...
```

Where:
- `<patch_name>` is the shortname of the patch to apply (as defined in the `<patch>.info` file)
- `<arg_name>` is the name of the argument to set (as defined in the `<patch>.info` file)
- `<arg_value_1>, <arg_value_2>, ...` are the values to use for the argument. The number of values defines the number of configuration alternatives to generate.
- The `n: '{}'` entry will be treated as the unmodified program.

*Note:* The identifier for each row needs to be incrementing, starting with 0 for the first row. This is a technical requirement of the VaRA-TS.

## Running Experiments

The VaRA-TS uses the `vara-run` command to run experiments.
The general syntax is:

```bash
vara-run -E <experiment_name> [--slurm] [--container] <case_study...>
```

Where:
- `<experiment_name>` is the name of the experiment to run (Supported experiment names are explained in the following subsections)
- `--slurm` is an optional flag that enables the generation of a slurm script to run the experiments on a cluster managed by slurm
- `--container` is an optional flag that enables running experiments inside a container
- `<case_study...>` are one or multiple case studies to run the specified experiment for. Available are:
    - `7zip`
    - `DunePerfRegression`
    - `libzmq`
    - `libvpx`
    - `x264`
    - `brotli`
    - `bzip2`
    - `ect`
    - `gzip`
    - `lepton`
    - `lrzip`
    - `xz`
    - `duckdb`
    - `mariadb`
    - `postgresql`
    - `HyTeg`
    - `FastDownward`
    - `cadical`
    - `cryptominisat`

### Finding Candidate Locations (`FindHiddenConfigurationPoints`)
The `FindHiddenConfigurationPoints` is used to run the AST matching tool to find candidate locations for hidden configuration opportunities.
It requires that the AST matching tool is installed and available in the VaRA-TS environment.
Its' results are stored in JSON files in the case-study specific `results` directory.

### Collecting Coverage Information (`CollectBinaryCoverages` and `BenchbaseCoverage`)
The `CollectBinaryCoverages` experiment is used to collect the coverage of workloads for each case study.
For projects using Benchbase as their workloads (`mariadb`, `postgresql`), the `BenchbaseCoverage` experiment is used instead.
Its' results are stored in JSON files in the case-study specific `results` directory.

### Filtering Candidate Locations (`FilterHiddenConfigurabilityReport`)
The `FilterHiddenConfigurationPoints` experiment is used to filter the candidate locations found by the `FindHiddenConfigurationPoints` experiment.
It uses the coverage data collected by the `CollectBinaryCoverages` and `BenchbaseCoverage` experiment.
The output format are JSON files with the same format as for the `FindHiddenConfigurationPoints` experiment, with additional tags for excluded locations.

### Testing configuration alternatives (`TestPatchVariations`)
This experiment runs the tests for each configuration alternative on the specified case studies, as well as the unmodified program.
Running this experiment requires that the case study has properly defined configuration alternatives.

### Measuring performance of Configuration Alternatives (`TimePatchedWorkloads`, `RunPatchedWorkloads`, `BenchbaseHiddenConfig`)
These experiments measures the performance of each configuration alternative on the specified case studies, as well as the unmodified program.
Running this experiment requires that the case study has properly defined configuration alternatives.

Most case studies use the `TimePatchedWorkloads` experiment, while the `BenchbaseHiddenConfig` experiment is used for case studies that use Benchbase as their workloads (`mariadb`, `postgresql`).
For `duckdb` we use the `RunPatchedWorkloads` experiment.

# Annotating Candidate Locations
To manually investigate the candidate locations that are the result of the `FindHiddenConfigurationPoints` or `FilterHiddenConfigurabilityReport` experiments, we used GitHub Copilot to develop a plugin for the JetBrains IDE.
It can be found in its' own [repository](https://github.com/LuAbelt/FindingsNavigator).

Once installed, users can select a JSON file with results for the specific case study. The plugin then offers a small navigator widget listing all found locations. When opening a JSON file while having the corresponding project open, it offers additional editor highlighting and navigating to specific results by double-clicking. The plugin can filter based on assigned tags and assign new tags to locations.
