This is a Drupal project. Follow Drupal conventions in every change:

- Drupal coding standards (the `Drupal` and `DrupalPractice` phpcs rulesets): 2-space indent,
  docblocks on every function, method and class, `t()` / `$this->t()` for user-facing strings.
- Use dependency injection in services, controllers, forms and plugins. Don't add new
  `\Drupal::service()` calls in classes that can take the service in their constructor.
- Configuration: if you change anything that lives in config (fields, views, settings, roles,
  permissions), change the YAML under `config/sync` (or the module's `config/install` /
  `config/optional`) as well. Never leave config only in the database.
- Schema: new config keys need a matching entry in `config/schema/*.schema.yml`.
- Existing sites: a change to config shipped in `config/install`, an entity type, a field
  storage or a database table needs a `hook_update_N()` (or a `hook_post_update_NAME()` for
  content changes) so existing sites get it. Never edit an update hook that has been released.
- Caching: render arrays that depend on a user, route, query argument, entity or config need
  the right `#cache` contexts, tags and max-age (`CacheableMetadata`, `addCacheableDependency()`).
  When you save data that is shown elsewhere, invalidate its cache tags.
- Security: database queries through the query builder or placeholders, never string
  concatenation; output through Twig or `#plain_text` / `Xss::filter()`; new routes need an
  `_permission`, `_access` or custom access check; forms keep Form API CSRF protection.
- Don't touch `core/`, `vendor/`, contrib modules or `web/sites/*/settings*.php`.
