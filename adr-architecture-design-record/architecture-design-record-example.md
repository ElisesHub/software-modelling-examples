

# 1. Use Dapper for read-heavy queries

Date: 2026-09-24

## Status
Accepted

## Context
Listing pages run complex read queries across several tables. EF Core's
change tracking adds overhead we don't need for read-only data. Dapper is quicker and easier to work with than ADO.Net and separate stored procedures as everything stays in the same place. 

## Decision
Use Dapper with hand-written SQL for read-only queries. Keep EF Core for
writes, where change tracking and migrations are valuable.

## Consequences
- Read queries are explicit and easy to optimise.
- Two data-access approaches in one codebase; developers need to know which to use.
- SQL in read queries isn't checked at compile time, so it needs integration tests.