# Terraform automation using GitHub Actions

This project contains workflows definitions which can help you to automate your infrastructure deployments.

This repository is relying on 2 external GitHub actions:

- [Manual Workflow Approval](https://github.com/trstringer/manual-approval)
- [Terraform GitHub Actions](https://github.com/dflook/terraform-github-actions)

If you want to know more, please watch [this video](https://youtu.be/QpRfZxUUinc).

<BlockComponent
block={{"owner":"ElijahPepe","repo":"youtube-block","id":"youtube-block","type":"file"}}
context={{"repo":"terraform-github-actions","owner":"AjTiTi","path":"youtube.txt","sha":"feat/github-blocks","file":"README.md"}}
height={453}
/>
## [Generate plan on PR](./.github/workflows/generate-plan-on-pr.yml)

This workflow generates the terraform plan for the dev environment when one of the developers opens a new pull request. After the plan will be succesfully generated, it will be shown as a comment in the pull request, so the developer can review the code and the impact it will make in the cloud at the same time.

<BlockComponent
block={{"type":"file","id":"ide-block","title":"IDE Block","description":"Block providing (readonly) editor tooling like tooltips and symbol navigation","entry":"blocks/ide-block/index.tsx","matches":["*"],"sandbox":false,"example_path":"https://github.com/Krzysztof-Cieslak/RustSample/blob/main/src/main.rs","owner":"Krzysztof-Cieslak","repo":"IDE-Block"}}
context={{"repo":"terraform-github-actions","owner":"AjTiTi","path":".github/workflows/generate-plan-on-pr-comment.yml","sha":"feat/github-blocks","file":"README.md"}}
/>

## [Generate plan on PR comment](./.github/workflows/generate-plan-on-pr-comment.yml)

This workflows generates the terraform plan for the dev environment when the developer writes `terraform plan` comment in the pull request comments section. It helps when the initial plan failed for some reason and you want to re-generate it within the same pull request.

## [Apply after merge](./.github/workflows/apply-after-merge.yml)

This workflow is running once the pull request will be merged to the main branch. It generates again the plan, compares it with approved one from the pull request, and if there no mismatches, applies it to the cloud.

<BlockComponent
  block={{
    owner: "Krzysztof-Cieslak",
    repo: "IDE-Block",
    id: "ide-block",
    type: "file",
  }}
  context={{
    path: ".github/workflows/apply-after-merge.yml"
  }}
/>

## [Release](./.github/workflows/release.yml)

This workflow is running when the new release is created and it contains 3 jobs:

1. Plan - generates the plan for the production environment and upload it to the artifacts.

1. Approve - creates an issue in GitHub repository with the plan and waits until it will be approved or canceled.

1. Apply - once the plan is approved, it applies the changes to the production environment.

<BlockComponent
block={{"owner":"Krzysztof-Cieslak","repo":"IDE-Block","id":"ide-block","type":"file"}}
context={{"repo":"terraform-github-actions","owner":"AjTiTi","path":".github/workflows/release.yml","sha":"HEAD","file":"README.md"}}
/>
