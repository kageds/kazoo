# Kazoo PropEr

[PropEr](http://proper.softlab.ntua.gr/) quickcheck models for various parts of Kazoo.

## Crossbar

I like to set console level to critical (chatty otherwise): `kazoo_maintenance:console_level(critical).`

After each quickcheck, I like to clean soft-deleted account docs from the `accounts` database: `kt_cleanup:cleanup_soft_deletes(<<"accounts">>).`

Also, clearing the data traces is good to do: `kz_data_tracing:clear_all_traces().`

### Skeleton

`pqc_cb_skels` contains a basic module for testing the CRUD-iness of an API endpoint. Copy the source to a new file for named for the API endpoint, change references to "skels" and "skel" to match the endpoint (say "devices" and "device") and modify the "new_{entity}" function to create a bare-minimum version of the entity for creation.

### [Phone Numbers](https://github.com/2600hz/kazoo/blob/master/core/kazoo_proper/src/pqc_cb_phone_numbers.erl)

Tests the [`phone_numbers`](/applications/crossbar/doc/phone_numbers.md) API

Sequential tests: `proper:quickcheck(pqc_cb_phone_numbers:correct()).`
Parallel tests: `proper:quickcheck(pqc_cb_phone_numbers:correct_parallel()).`

Cleanup deleted account docs: `kt_cleanup:cleanup_soft_deletes(<<"accounts">>).`

### [Ratedecks](https://github.com/2600hz/kazoo/blob/master/core/kazoo_proper/src/pqc_cb_rates.erl)

Tests the ratedeck upload task and rating a DID against account-vs-system ratedecks.

Run a quick sequential test: `pqc_cb_rates:seq()`

### [IPs](https://github.com/2600hz/kazoo/blob/master/core/kazoo_proper/src/pqc_cb_ips.erl)

Tests the dedicated IPs endpoint.

### [Recordings](https://github.com/2600hz/kazoo/blob/master/core/kazoo_proper/src/pqc_cb_recordings.erl)

Tests fetching recordings
