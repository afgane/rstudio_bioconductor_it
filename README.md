# rstudio_bioconductor_it
Galaxy Interactive Tool for RStudio with Bioconductor.

# Tool update process

1. Update the Docker image by making a PR to
   https://github.com/Bioconductor/bioconductor_docker/tree/devel/extensions/galaxy
2. Once the PR is merged, a Docker image
   ((bioconductor/galaxy-rstudio)[https://hub.docker.com/r/bioconductor/galaxy-rstudio/tags])
   will be automatically built. Then, update the tool XML file to reference the
   new image version. Make any other necessary changes to the tool XML.
3. From the repo root folder, run the following command to check the diffs with
   the ToolShed:
   ```
   planemo shed_diff --shed_target toolshed interactive_tool_rstudio_bioconductor/
   ```
4. Run the lint command locally:
   ```
   planemo shed_lint --tools --ensure_metadata --urls --report_level all --fail_level error --recursive interactive_tool_rstudio_bioconductor
   ```
5. Create a branch, commit the changes, and push to GitHub. Then open a PR in this repo,
   which will trigger a CI workflow to update the tool on the Toolshed.

# Local container testing

Build the Docker image locally with:

```
docker build --platform linux/amd64 -t afgane/bioconductor_docker:RELEASE_3_23 .
```

Run the container with:

```
docker run -p 8787:8787 -e PASSWORD=bioc -d afgane/bioconductor_docker:RELEASE_3_23
```

The container will be available at http://localhost:8787 with username `rstudio` and password `bioc`.
