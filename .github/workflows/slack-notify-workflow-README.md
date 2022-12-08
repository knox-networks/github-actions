# slack-notify-workflow-invoked / slack-notify-workflow-finished

This document describes the usage details for the `slack-notify-workflow-invoked` and `slack-notify-workflow-finished`
callable workflows. These two workflows are designed to act as bookends to existing GHA workflows to notify of `started`
and `finished` events rather than having to inject inline Slack notification actions throughout various stages/jobs of
your GHA pipelines.

## slack-notify-workflow-invoked

The `slack-notify-workflow-invoked` GHA workflow is a callable workflow intended to update the corporate `#deployment`
Slack channel that a GHA workflow has been started. This workflow is intended to be called as the _very first job_
within your GHA pipeline and can be executed simultaneously along with your initial pipeline operation.

### Usage

```yaml
jobs:
  call-notify-slack-workflow-invoked:
    name: Notify Slack
    uses: knox-networks/github-actions/.github/workflows/slack-notify-workflow-invoked.yml@main
    secrets:
      slack-bot-token: ${{ secrets.SLACK_BOT_TOKEN }}
```

### Secrets

| Variable Name     | Description                             |
|-------------------|-----------------------------------------|
| `slack-bot-token` | Slack Bot channel authentication token. |

### Outputs

| Variable Name      | Description                                                                |
|--------------------|----------------------------------------------------------------------------|
| `slack-message-id` | Slack channel message ID (to be used in `slack-notify-workflow-finished`). |

## slack-notify-workflow-finished

The `slack-notify-workflow-finished` GHA workflow is a callable workflow intended to notify the corporate `#deployment`
Slack channel that a GHA workflow has finished with either a `success` or `failure` result.

If the optional `slack-message-id` input variable is assigned with the output `slack-message-id` value from
`slack-notify-workflow-invoked.output.slack-message-id`, the notification message for `success` or `failure` will
update the original message posted from the `slack-notify-workflow-invoked` workflow. Doing this can cut down on the
overall number of messages across GHA workflow invocations and treat Slack messages in the `#deployment` channel as
status updates for a GHA pipeline rather than posting separate messages per notification.

### Usage

_The following example reuses the `slack-message-id` from the `slack-notify-workflow-invoked` workflow. Also note the_
_value for the `workflow-succeeded` input variable. Sometimes this can be expressed as a simple expression, whereas_
_other evaluations of a succeeded/failed workflow might require more logic depending if certain actions are `skipped`,_
_etc._

```yaml
jobs:
  call-notify-slack-workflow-invoked:
    name: Notify Slack
    uses: ./.github/workflows/slack-notify-workflow-invoked.yml
    secrets:
      slack-bot-token: ${{ secrets.SLACK_BOT_TOKEN }}

  build:
    name: Code Build
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
      - name: Build / Test
        run: echo "building and testing some stuff..."

   call-notify-slack-workflow-finished:
    name: Notify Slack
    uses: ./.github/workflows/slack-notify-workflow-finished.yml
    if: always()
    needs:
      - call-notify-slack-workflow-invoked
      - build
    with:
      workflow-succeeded: ${{ (needs.build.result == 'success' || needs.build.result == 'skipped') }}
      slack-message-id: ${{ needs.call-notify-slack-workflow-invoked.outputs.slack-message-id }}
    secrets:
      slack-bot-token: ${{ secrets.SLACK_BOT_TOKEN }}
```

### Inputs

| Variable Name        | Type    | Description                                                                                       |
|----------------------|---------|---------------------------------------------------------------------------------------------------|
| `slack-message-id`   | string  | Slack Message ID (from `notify-slack-workflow-invoked.outputs.slack-message-id`).                 |
| `workflow-succeeded` | boolean | Boolean value indicating wheither or not all of the prior workflow jobs have succeeded or failed. |

### Secrets

| Variable Name     | Description                             |
|-------------------|-----------------------------------------|
| `slack-bot-token` | Slack Bot channel authentication token. |

## References

* [GHA Action: klamas1/github-action-slack-notify-build](https://github.com/klamas1/github-action-slack-notify-build)
* [Slack Tokens](https://api.slack.com/authentication/token-types)
