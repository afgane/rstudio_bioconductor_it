# rstudio_bioconductor_it
Galaxy Interactive Tool for RStudio with Bioconductor.

# Tool update process

1. Update the Docker image via
   https://github.com/Bioconductor/bioconductor_docker/tree/devel/extensions/galaxy
2. Once a Docker image is built and available, update the tool XML file to
   reference the new image version. Make any other necessary changes to the tool XML.
3. From the `interactive_tool_rstudio_bioconductor` folder, run the following
   command to check the diffs with the ToolShed:
   ```
   planemo shed_diff --shed_target toolshed
   ```
4. Run the lint command locally, from the repo's parent dir:
   ```
   planemo shed_lint --tools --ensure_metadata --urls --report_level all --fail_level warn --recursive interactive_tool_rstudio_bioconductor
   ```
5. Create a branch, commit the changes, and push to GitHub. Then open a PR,
   which will trigger a CI workflow to update the tool on the Toolshed.
