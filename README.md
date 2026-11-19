# omni-change-demo

Sample repo that generates commits, PRs, releases and GitHub Deployments for testing Change Indicators in Amazon CloudWatch Omni.

## Setup
1. Create an empty repo `omni-change-demo` on github.com under an org you own.
2. Push this folder:
   git init && git add -A && git commit -m "init"
   git branch -M main
   git remote add origin git@github.com:<org>/omni-change-demo.git
   git push -u origin main
3. Settings > Environments: create `staging` and `production`.
4. Settings > Actions > General: set Workflow permissions to "Read and write" (needed by churn.yml).

## What generates changes
- deploy.yml: every push to main deploys to staging. Run it manually to target production.
- churn.yml: commits a timestamp every 2 hours (or run manually), which triggers a deploy.

## Extra test cases
- Open and merge PRs that edit config.json (for example "feat: change retry timeout").
- Tag a release: git tag v0.1.0 && git push --tags, then publish it on GitHub.
- Failed deploy: add `exit 1` to the Fake deploy step, push, then revert.

## Connect to Omni
Add GitHub connection > GitHub.com, install the Amazon CloudWatch app on this repo, then map the repo to a service in Service Catalog if needed.
