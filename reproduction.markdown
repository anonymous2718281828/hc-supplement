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

## AST Pattern Matching Tool
TODO

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
To generate a specific arteface with the same options as used in the paper, and on this website, run the following command in the VaRA-TS environment:
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
