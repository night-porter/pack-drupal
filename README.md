# Night Porter pack: Drupal

Drupal coding standards (phpcs `Drupal`/`DrupalPractice`, phpstan), config export, update hooks, cache metadata and Drupal security basics, plus a DDEV environment preset.

A [Night Porter](https://night-porter.com) pack: prompts only, no code. Like every pack it can
only make Night Porter stricter: it adds instructions and read-only gates, and can't skip its
trust rules, checks or approvals.

```sh
nightporter market update
nightporter pack add drupal
```

Then enable it in `[defaults]` or a repo file (`repos/<forge>/<owner>/<repo>.toml`):

```toml
packs = ["drupal"]
```

| step | hook | what it does |
|---|---|---|
| `standards` | `pre_fix` | Drupal conventions: DI, config + schema, update hooks, cache tags/contexts, safe queries and output |
| `lint` | `post_fix` | runs phpcs, phpstan and `drush config:status` on changed files (via DDEV if present) |
| `review` | `pre_push` | blocks unsafe SQL/output, unprotected routes, edits to core/contrib/released update hooks; asks before update hooks, schema changes, unexported config or missing cache metadata |

The agent can only run commands you allow. For a DDEV project, in the repo file:

```toml
sandbox = false   # DDEV needs the Docker socket
allow_commands = ["ddev exec", "ddev drush", "ddev phpunit", "ddev composer"]
```

## DDEV preset

`nightporter pack env drupal/ddev` prints an `[env]` table that starts a DDEV stack per
worktree (`drupal11`; change to `drupal10` if needed). Paste it into the repo file.

Read every file before installing: they steer an agent that can edit your code. See
[Writing packs](https://docs.night-porter.com/writing-packs).

Licensed under either of Apache-2.0 or MIT, at your option.
