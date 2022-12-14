# Actions and Workflows

This repository contains a collection of actions and workflows that can be used in your GitHub Actions and Workflows.
It tests, builds, creates pull requests and deploys preprod/prod environments to Firebase while notifying your Slack channel after each action (e.g., test, build, create PR, deployment) with its status (e.g., success, fail). Messages and workflows are highly customizable.


It also contains set of actions from the [GitHub Actions Marketplace](https://github.com/marketplace?type=actions). 
They are:
- [actions/checkout@v3](https://github.com/marketplace/actions/checkout)
- [tj-actions/branch-names@v6](https://github.com/marketplace/actions/branch-names)
- [actions/setup-node@v3](https://github.com/marketplace/actions/setup-node-js-environment)
- [rtCamp/action-slack-notify@v2](https://github.com/marketplace/actions/slack-notify)
- [devops-infra/action-pull-request@v0.5.0](https://github.com/marketplace/actions/github-action-for-creating-pull-requests)
- [FirebaseExtended/action-hosting-deploy@v0](https://github.com/marketplace/actions/deploy-to-firebase-hosting)

## Workflow
- Test `feature/*` branch on push to remote
- Notify Slack channel on test success/fail
- If test success, create pull request from `feature/*` to `master` branch
- Notify Slack channel on pull request creation success/fail
- If create PR success, deploy this `feature/*` branch to preproduction environment. The deployment link is sent to the Slack channel.
- Notify Slack channel on deployment success/fail
- Merge pull request to `master` branch _(this is manuel action)_
- Test `master` branch on push to `master`
- Notify Slack channel on test success/fail
- If test success, deploy `master` branch to production environment. The deployment link is sent to the Slack channel.
- Notify Slack channel on deployment success/fail

## Usage
To use this workflow, you can copy the entire [.github](.github) folder and paste it into your root directory.
Then, you can modify the workflows to suit your needs.

You need to create a [GitHub Secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository) named;
- `CHANNEL_NAME` and set its value to your Slack channel name. (e.g., general, random)
- `PAT` and set its value to your GitHub Personal Access Token. Needs to have repo scope access. Refer [here](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
- `SLACK_WEBHOOK` and set its value to your Slack webhook URL. Get one [here](https://slack.com/apps/A0F7XDUAZ-incoming-webhooks).
- `FIREBASE_SERVICE_ACCOUNT` and set its value to your Firebase token. Create one [here](https://github.com/marketplace/actions/deploy-to-firebase-hosting#setup).

You can provide your Slack Message icon by modifying the `SLACK_ICON` in the [slack-notifier](.github/actions/slack-notifier/action.yml) file.
Please refer the action links above for more information and customization. 


To use custom emojis in your Slack notification, you can use [this](https://slackmojis.com/) list. 
Download emojis you want to use and upload them to your Slack workspace. 
Then, you can use them in your Slack notification text.

#### Screenshots
On test success after merge to `master` branch

![Slack notification on success](images/success.png)

On test fail on `feature/instagram` branch

![Slack notification on fail](images/fail.png)
