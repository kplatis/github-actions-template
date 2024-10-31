# Github Actions Template


## Protecting Main Branches

Setting up branch protection rules helps prevent unauthorized changes to important branches, like `main` and `dev`, by enforcing pull requests and status checks.

### Steps
1. Go to your repository's **Settings**.
2. Under **Code and automation**, select **Branches**.
3. Create a new **branch protection rule**:
   - Click **Add branch protection rule**.
4. In **Branch name pattern**, specify the branch(es) to protect (e.g., `main`, `dev`).
5. Configure the following options:
   - **Require a pull request before merging**: This requires a pull request and at least one review before merging.
   - **Require status checks to pass before merging**: Enforces that all required status checks (like GitHub Actions workflows) pass before merging.

### Additional Options (optional but recommended)
   - **Require signed commits**: Enforces commit signing for added security.
   - **Restrict who can push to matching branches**: Limits push access to specific team members or roles.

---

## Setting Secrets

GitHub allows us to securely store secrets (such as API keys or tokens) for use within GitHub Actions workflows. Secrets are encrypted and accessible only to workflows and authorized services.

### Steps
1. In your repository, navigate to **Settings**.
2. Go to **Secrets and variables** and select **Actions**.
3. Click **New repository secret** to add a new secret.
4. Enter a **Name** for the secret (e.g., `API_KEY`) and the **Value** (the secret value itself).
5. Click **Add secret** to save.

### Important Notes
- **Secrets are not logged**: The values are hidden in workflow logs to protect sensitive information.
- **Secrets must be carefully named**: Use descriptive names for easy management (e.g., `DATABASE_PASSWORD` or `AUTH_TOKEN`).

### Using Secrets in Workflows
Secrets can be accessed in GitHub Actions workflows as environment variables:

```yaml
# .github/workflows/example.yml

jobs:
  example-job:
    runs-on: ubuntu-latest
    steps:
      - name: Run a step that uses a secret
        run: echo "The API key is ${{ secrets.API_KEY }}"
```

---

## Securing Pull Requests from Exposing Secrets

By default, GitHub Actions workflows run on pull requests. However, secrets can be exposed if a pull request comes from an untrusted source (e.g., a forked repository). 

### Steps to Secure Forked Pull Requests
1. In your repository, go to **Settings**.
2. Under **Actions**, navigate to **General**.
3. Enable **Run workflows from fork pull requests**.
4. Set **Fork pull request workflows from outside collaborators** to **Require approval for all outside collaborators**.

   - This requires approval from a repository owner or collaborator before workflows run, ensuring that secrets aren’t exposed to untrusted forks.

### Additional Tips
- **Regularly review** and rotate secrets to maintain security.
- **Audit access** to your repository settings to prevent unauthorized changes.

---

Following these steps ensures secure branch protections, secret management, and workflow safeguards against potential security risks.
