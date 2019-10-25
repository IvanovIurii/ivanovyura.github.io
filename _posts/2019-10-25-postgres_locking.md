---
layout: post
title: Postgres Locking Notes
author: Iurii Ivanov
tags: [postgres, lock]
---

...

*Disclaimer*: this is not a tutiorial, just some notes to myself to know what to google, if I need to work with locks.
This article will be changing during the time, when I come back to locks from time to time... or not.

Computers rignt now have more than one CPU, so it is possible to run queries in parallel,
so if we operate in different transactions, with the same resource,
we need to know how not to access this resource at the same time, we need locks. It is important nowadays at least basically 
undersatnd how it works. 

Plus it is not only about parallels, it is also about threads. Anyway, even if we need access resiurces concurrently, it is 
still important to know locking.

Another thing to remember is that even a simple transaction will create a bunch of table locks. 
And actually all the time before an SQL statement uses a table,
it takes the appropriate table lock.
For example, reading from a table will take a `ACCESS SHARE`
lock which will conflict with the `ACCESS EXCLUSIVE` lock that `TRUNCATE` needs (`DELETE` statement).

But this note is about explicit locks.
There are also implicits, bit it is later...

In this one I just touch table locks (`LOCK TABLE` statement).
But for example, when we do simple `SELECT` or update database, or alter columns, etc., we have locks even without knowing.

So, about table locks...

There are 2 types of locks - table and row level.

Most of the time table level locks are for maintenance tasks (backups/schema changes/migrations), I guess...

Postgres has a special mechanism, called MVCC – Multi-Version Concurrency Control, to ensure data integrity during multiple
concurrent read/write operations in different transactions. It is necessary,
because it helps to maintain different versions of updated row/resource and do everything in proper order.

Most of the time you do not need to do an explicit lock,
Postgres does it automatically, unless you need to write and read to/from the same row simultaneously
(transfer/send money at the same time, i.e.).

But explicit locking can be useful also in bulk update, to avoid deadlocks with other transactions,
or some data lost: `SHARE LOCK` - it prevents concurrent data modifications, `LOCK TABLE <table> IN SHARE MODE`;

---

Another thing to remember... I already mentioned about lock if we do transfer/top up money concurrently for the same user
(one row), we may need to lock the row. If you don’t want concurrent transactions to modify a row between
the time you read it and the time you update:

`SELECT ... FOR UPDATE`

Example: two concurrent transactions are trying to select a row for update.

If a statement is trying to to modify the same row, it checks the list of unfinished transactions.
The statement has to wait for modification until the previous transaction is finished (*TBD*: see xmax and xmin).

The `SELECT FOR UPDATE` query running in the second connection is unfinished,
and waiting for the first transaction to complete.

---

But if concurrent modifications are unlikely and you are not sure that you are actually going to modify the row,
a `REPEATABLE READ` transaction may be even better. 
That means that you have to be ready to retry the operation if the `UPDATE` fails due to a serialization error.

---

If you need to get a row from a table, process it and then remove it? Use `DELETE ... RETURNING`, then the row will be locked immediately!

---

`PG_LOCKS` - system view to see current locks. View is a pseudo-table. They are "not real", but they are available for `SELECT`.

---

There are several lock modes.

If no lock mode is specified, then `ACCESS EXCLUSIVE`, 
the most restrictive mode, is used (when you use `LOCK TABLE <table>` without mode).
Table is locked (with `ACCESS EXCLUSIVE`),
until the transaction ends and to finish the transaction you will have to either rollback or commit the transaction.

- ACCESS SHARE --> SELECT
- ROW SHARE
- ROW EXCLUSIVE
- SHARE UPDATE EXCLUSIVE
- SHARE
- SHARE ROW EXCLUSIVE
- EXCLUSIVE
- ACCESS EXCLUSIVE --> TRUNCATE for example

*NOTE:* The `LOCK` statement works only in a transaction mode.

List of Content:

https://www.compose.com/articles/common-misconceptions-about-locking-in-postgresql/
https://www.cybertec-postgresql.com/en/lock-table-can-harm-your-database/
https://www.postgresql.org/docs/current/explicit-locking.html#LOCKING-TABLES
http://www.interdb.jp/pg/pgsql05.html
