# Development Manifest

1. **Follow LEAN & KISS**
    - Do not overthink and over-engineering
    - Do not anything because "it's cool"
    - Do not anything "just in case"
    - Do only what business needs right now and maybe 2-4 weeks ahead
    - Always ask "Why we need this?" question
    - Create new features that are **easy to remove**
    - Be consistent
    - Follow "scout" rule → https://deviq.com/principles/boy-scout-rule
    - Continuously track and reduce technical debt

2. **Plan your work**
    - Always discuss the data model before adding new entities or attributes
    - Before every major change, prepare an RFC document
    - Implement it step by step (table by table, column by column)
    - Separate business logic and DB migration into separate PRs
    - Do not create unnecessary tables and columns that are not required in a current moment of time
    - Avoid exposing primary sequential `ID` at `API` level
    - Use `uid` column as `ULID` format → https://github.com/rafaelsales/ulid
    - GraphQL query for collection must always return nodes field as future pagination should be allowed
    - For classes use formal naming with suffixes: `FooType`, `BarService`, `BazMutation`
    - Keep domain language consistent between code, DB and API

3. **TDD is the boss**
    - Keep coverage close to 100%
    - Always cover happy path and 1-3 sad cases
    - One app file should have one test file
    - Use shared helpers or custom matchers → https://thoughtbot.com/blog/shoulda-matchers
    - Try to avoid hash_including and use only for difficult cases
    - Do not use after_create in traits
    - Split large test file to smaller with context _suffix. Like `items_query_spec.rb + items_qudery_filter_spec.rb + items_query_pagination_spec.rb`, etc.
    - Use built-in custom matchers for dry specs
    - Carefully use shared examples: good naming, the minimum amount of params, subject-related checks

5. **SQL**
    - Always use database transactions for operations that modify multiple records
    - Avoid paginating records using OFFSET - use cursor-based pagination (WHERE id > last_id) instead
    - Use database constraints (NOT NULL, UNIQUE, CHECK) at the database level, not just in application code
    - Always add rollback logic for destructive migrations
    - Monitor and optimize slow queries using *EXPLAIN ANALYZE* 
    - De-normalize schema with the PG materialized views → https://github.com/scenic-views/scenic
    - Use Postgres Enums → https://github.com/bibendi/activerecord-postgres_enum
    - Use database-level locking (SELECT FOR UPDATE) when dealing with race conditions
    - Use database-level unique constraints instead of application-level uniqueness checks for critical data
    - Follow the https://wiki.postgresql.org/wiki/Don't_Do_This

6. **Use microservices wisely**
    - Each microservice should own its database - avoid shared databases between services
    - Implement retry logic with exponential backoff for transient failures
    - Use distributed tracing to track requests across service boundaries
    - Design services around business capabilities, not technical layers
    - Prefer asynchronous communication (events) over synchronous when possible
    - Use RPC for synchronous communication between microservicese
    - Implement health checks and readiness probes for all services
    - Make sure that kafka consumers are idempotent

7. **Be nice**
    - Use static code analyzers like https://github.com/rubocop/rubocop or https://github.com/standardrb/standard
    - Don't turn off the analyzers rules for no reason
    - Use emoji (like https://github.com/bgian/slack-emojis) to share progress updates and respond to posts
    - Write self-descriptive commit messages with answers on "what and why"
    - Open PR's and ask about feedback. Do not push with force. Squash commits on merge.
    - Do not shy to comment your code with local README.md file
    - Be kind to create new tips and docs
    - Refactor continuously, not in big-bang rewrites


**Extra resources**
- https://37signals.com/00
- https://deviq.com/
- https://www.writesoftwarewell.com/
- https://blog.bytebytego.com/