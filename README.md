### Example: using the envTemplate tag policy

This example reuses the image name and uses both dateTime and gitCommit tagging strategies.
The way you configure it in `skaffold.yaml` is the following build stanza:

```yaml
build:
  artifacts:
  - image: skaffold-example
  tagPolicy:
    userDefined:
      template: "{{.IMAGE_NAME}}:{{.DATE}}_{{.GIT}}"
      components:
      - name: DATE
        dateTime:
          format: "2006-01-02"
          timezone: "UTC"
      - name: GIT
        gitCommit:
          variant: AbbrevCommitSha
```

1. define `tagPolicy` to be `userDefined`
2. use [go templates](https://golang.org/pkg/text/template) syntax
3. The `IMAGE_NAME` variable is built-in and reuses the value defined in the artifacts' `image`.
4. define the components referenced in the template and then the tagging strategy below the name along with its variations