# Github Actions Template


## How to protect main branches

1. Access `Settings`
2. Create a new ruleset in `Rules > Ruleset`
3. Add the `main` and/or `dev` branch as a target branch
4. In the rules mark `Require a pull request before merging` and `Require status checks to pass`


## How to set a secret

1. Access repository `Settings`
2. Access `Secrets and variables > Actions` menu item
3. Add the secret. This value is not logged within the context of a Github action

### How to secure pull requests from exposing secret

1. Access `Settings`
2. Access `Actions > General` and mark `Run workflows from fork pull requests `
3. Under `Fork pull request workflows from outside collaborators` mark `Require approval for all outside collaborators`. This prevents outside collaborators from modifying the action to expose the secret