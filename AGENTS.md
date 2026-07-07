# fatzebra-PHP-Library

## What this is
A PHP client library for the Fat Zebra online payment gateway (Australian merchants), providing purchases, refunds, and recurring billing (subscriptions/plans/customers). It's a single-class library (`FatZebra.class.php`) plus a CA bundle for TLS verification, upstream from Fat Zebra with a Hey You-side release cut.

## IMPORTANT: name mismatch
The **repository name** is `fatzebra-PHP-Library`, but the **published Composer package name** is `heyyou/fatzebra-php` (see `composer.json`). These do not match. Do not assume you can find this dependency by searching for "fatzebra-PHP-Library" in another repo's `composer.json` — search for `fatzebra-php` (or `FatZebra.class.php`) instead.

## Published package
`heyyou/fatzebra-php`, version `1.2.10`.

## Consumer and pin
Consumed by the `api` monolith as a Composer VCS dependency:
- `api/composer.json` → `repositories` entry: `git@github.com:heyyou/fatzebra-PHP-Library.git`
- `api/composer.json` → `require`: `"heyyou/fatzebra-php": "1.2.10"`
- `api/composer.json` → `autoload.classmap`: `["vendor/heyyou/fatzebra-php/FatZebra.class.php"]`

Note it's loaded via Composer's classmap autoloading (no PSR-4/PSR-0 namespace), pointing at a specific file path inside `vendor/heyyou/fatzebra-php/`. Renaming the class file or moving it out of the repo root would break `api`'s classmap even if the package name and version stayed the same.

## Status
Not fully frozen like the other libraries in this group — this fork has seen recent activity (most recent commit Oct 2025, "refactor/update-sandbox-url"), so treat it as low-churn/maintained rather than dead. Still small and load-bearing.

## Do not delete or rename
Do not delete or rename this GitHub repository, and do not rename `FatZebra.class.php` or move it out of the repo root. `api` depends on both the exact VCS URL and the exact classmapped file path.

## How a change would propagate
`api` pins an exact version (`1.2.10`), so changes here do NOT automatically reach `api`. To ship a change:
1. Cut a new tag/version in this repo (update `composer.json` `version` too, since it's read directly rather than via git tags in some flows — verify against how this repo has been versioned historically).
2. Bump the version constraint in `api/composer.json` (`heyyou/fatzebra-php`).
3. Run `composer update heyyou/fatzebra-php` in `api` and commit the updated `composer.lock`.
