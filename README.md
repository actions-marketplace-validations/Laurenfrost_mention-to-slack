# Convert Github mention to Slack mention

!!! This action modified from [actions-mention-to-slack](https://github.com/abeyuya/actions-mention-to-slack) !!!

This action sends mention to your slack account when you have been mentioned at github.

## Feature

- Send mention to slack if you have been mentioned
  - pull request
- Send notification to slack if you have been requested to review.

## TODO

- Send mention to slack if you have been mentioned
  - pull request comments
  - issue
  - more and more

## Inputs

| Name | Required | Default | Description |
| :--- | :--- | :--- | :--- |
| configuration-path | Yes | .github/mention-to-slack.yml | Mapping config for Github username to Slack member ID. |
| slack-webhook-url | Yes | Null | Slack Incomming Webhook URL to notify. |
| repo-token | Yes | Null | Github access token to fetch .github/mention-to-slack.yml file. |
| github-event-name | Yes | Null | Event name that triggered the actions. |
| bot-name | No | Github Mention To Slack | Display name for this bot on Slack. |
| icon-url | No | Null | Display icon url for this bot on Slack. |
| run-id | No | Null | Used for the link in the error message when an error occurs. |

## Example usage

.github/workflows/mention-to-slack.yml

```yml
name: mention-to-slack-actions

on:
  issues:
    types: [opened, edited]
  issue_comment:
    types: [created, edited]
  pull_request:
    types: [opened, reopened, edited, closed, review_requested]
  pull_request_review:
    types: [submitted]
  pull_request_review_comment:
    types: [created, edited]

jobs:
  mention-to-slack:
    runs-on: ubuntu-latest
    steps:
      - name: Mention to Slack Actions
        uses: Laurenfrost/mention-to-slack@latest
        with:
          configuration-path: .github/mention-to-slack.yml
          repo-token: ${{ secrets.GITHUB_TOKEN }}
          slack-webhook-url: ${{ secrets.SLACK_WEBHOOK_URL }}
          github-event-name: ${{ github.event_name }}
          icon-url: https://github.githubassets.com/images/modules/logos_page/Octocat.png
          bot-name: ${{github.repository}}
          run-id: ${{ github.run_id }}
```

.github/mention-to-slack.yml

```yml
# For Github User
# github_username: "slack_member_id"

github_username_A: "slack_member_id_A"
github_username_B: "slack_member_id_B"
github_username_C: "slack_member_id_C"
abeyuya: "XXXXXXXXX"

# For Github Team
# github_teamname: "slack_member_id"

github_teamname_A: "slack_member_id_D"
```
