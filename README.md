# [@andrewmcodes](https://twitter.com/andrewmcodes)/actions

Composite Actions and Shared Workflows for GitHub Actions

[![Project Status: WIP – Initial development is in progress, but there has not yet been a stable, usable release suitable for the public.](https://www.repostatus.org/badges/latest/wip.svg)](https://www.repostatus.org/#wip)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
![GitHub commit activity](https://img.shields.io/github/commit-activity/m/andrewmcodes/actions)

## Installation

As of now, this is only meant for my personal use, and is WIP, but usage instructions are below that will ensure if you do use this, it won't change out from under you.

> **Warning**
> If you decide to use one of these actions, make sure to pin the action to a specific SHA or tag.

To be totally safe, you can fork this repo and use your own fork as the source of the action while I continue to iterate on this.

## Composite Actions

- Setup
  - `setup-node`
  - `setup-ruby`
- Linters
  - `brakeman`
  - `bundler-audit`
  - `standard`
- Release
  - `release-please-simple`

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

      - name: Setup Node
        uses: andrewmcodes/actions/setup-node@main

      - name: Bundler Audit
        uses: andrewmcodes/actions/bundler-audit@main

      - name: Brakeman
        uses: andrewmcodes/actions/brakeman@main

      - name: Standard
        uses: andrewmcodes/actions/standard@main
```

## Contributing

Contributions will be welcome once this becomes a little more stable.
