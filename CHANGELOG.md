# v1.0.0 - 2025-04-29 - Long overdue 1.0

### Notedworthy Changes:

* `SPF` record support removed, records should be migrated to `TXT` before
  upgrading.
* Requires octoDNS >= 1.5.0

## v0.0.4 - 2025-04-04 - Key changes

* Add global_key provider param to support disabling IP whitelisting

## v0.0.3 - 2024-11-29 - Delete w/o fail

* Deletion of records results in a stack trace in version 0.0.2.

## v0.0.2 - 2024-10-17 - More the merrier

#### Nothworthy Changes

* Added support for more record types: ALIAS, DS, NAPTR, TLSA, TLSA
* Added support for root nameservers

## v0.0.1 - 2022-01-14 - Moving

#### Nothworthy Changes

* Initial extraction of TransipProvider from octoDNS core

#### Stuff

Nothing
