# (WIP) [@andrewmcodes](https://twitter.com/andrewmcodes)/actions

Shared GitHub Actions for all of my projects.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![GitHub commit activity](https://img.shields.io/github/commit-activity/m/andrewmcodes/actions)

## Actions

- brakeman
- bundler-audit
- release-please-simple
- setup-ruby
- standard

## Installation

**🚨 DANGER 🚨**

This is still a work in progress and things are likely to change. If you decide to use one of these actions, make sure to pin the action to a specific SHA to ensure it doesn't change out from under you as I experiment.

## Usage/Examples

```yml
name: "Ruby on Rails CI"
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
jobs:
  test:
    runs-on: ubuntu-latest
    services:
      postgres:
        image: postgres:11-alpine
        ports:
          - "5432:5432"
        env:
          POSTGRES_DB: rails_test
          POSTGRES_USER: rails
          POSTGRES_PASSWORD: password
    env:
      RAILS_ENV: test
      DATABASE_URL: "postgres://rails:password@localhost:5432/rails_test"
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      # Add or replace dependency steps here
      - name: Setup Ruby
        uses: andrewmcodes/actions/setup-ruby@main
      # Add or replace database setup steps here
      - name: Set up database schema
        run: bin/rails db:schema:load
      # Add or replace test runners here
      - name: Run tests
        run: bin/rake

  lint:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Setup Ruby
        uses: andrewmcodes/actions/setup-ruby@main

      - name: Bundler Audit
        uses: andrewmcodes/actions/bundler-audit@main

      - name: Brakeman
        uses: andrewmcodes/actions/brakeman@main

      - name: Standard
        uses: andrewmcodes/actions/standard@main
```

## Contributing

Contributions will be welcome once this becomes a little more stable.
