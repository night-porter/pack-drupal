Check the PHP, YAML and Twig files you changed with the project's own tools. Prefer the DDEV
wrappers when there is a `.ddev/` folder (`ddev exec vendor/bin/phpcs ...`, `ddev exec
vendor/bin/phpstan ...`), otherwise run them directly:

- `vendor/bin/phpcs --standard=Drupal,DrupalPractice --extensions=php,module,inc,install,test,profile,theme,info,yml <changed files>`
  (or the project's `phpcs.xml(.dist)` if it has one).
- `vendor/bin/phpstan analyse <changed files>` when the project has a `phpstan.neon(.dist)`.
- `drush config:status` (or `ddev drush cst`) when you changed config and a site is installed,
  to confirm the YAML and the database agree.

Fix problems on lines you changed. Don't reformat untouched code, and don't add baseline or
ignore entries to make a check pass. If a tool isn't installed or you aren't allowed to run it,
say so in your summary instead of guessing.
