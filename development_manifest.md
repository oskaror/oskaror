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
    - Track and resolve any internal technical debt issues

2. **General data model plan**
    - Data model always can be discussed. Always discuss before adding something that is missing in the data model
    - Implement it step by step (table by table, column by column)
    - Separate business logic and DB migration into separate PRs
    - Do not create unnecessary tables and columns that are not required in a current moment of time
    - De-normalize schema with the PG materialized views → https://github.com/scenic-views/scenic
    - Use Postgres foreign keys → https://thoughtbot.com/blog/referential-integrity-with-foreign-keys
    - Use Postgres Enums → https://github.com/bibendi/activerecord-postgres_enum
    - Avoid exposing primary sequential `ID` at `API` level
    - Use `uid` column as `ULID` format → https://github.com/rafaelsales/ulid
    - GraphQL query for collection must always return nodes field as future pagination should be allowed
    - For classes use formal naming with suffixes: `FooType`, `BarService`, `BazMutation`
    - Use `rails credentials:edit --environment ...` (development/test/staging/production) for managing secrets
    - All money values must be in cents (!)
    - Follow the https://wiki.postgresql.org/wiki/Don't_Do_This

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
    
4. **Be nice**
    - Use static code analyzers like https://github.com/rubocop/rubocop or https://github.com/standardrb/standard
    - Don't turn off the rubocop rules for no reason
    - Use emoji (like https://github.com/bgian/slack-emojis) to share progress updates and respond to posts
    - Write self-descriptive commit messages with answers on "what and why"
    - Open PR's and ask about feedback. Do not push with force. Squash commits on merge.
    - Do not shy to comment your code with local README.md file
    - Be kind to create new tips and docs
    - Use the C4 model for creating architecture diagrams →  https://c4model.com/

### Extra **resources**

- https://37signals.com/00
- https://deviq.com/