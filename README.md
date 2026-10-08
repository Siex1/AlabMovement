# Alab Movement

Official repository for **Alab Movement**.

## Repository Structure

- **`production`**: Live production release branch connected to the production database environment.
- **`testing`**: Active testing and QA branch connected to the isolated testing database environment.

Refer to [BRANCHING_WORKFLOW.md](./BRANCHING_WORKFLOW.md) for full instructions on working with the two-way branch model.

## Environment & Database Setup

1. Copy the appropriate environment configuration:
   - For testing: Copy `.env.testing` to `.env`
   - For production: Copy `.env.production` to `.env`
2. Update your credentials in `.env` as required.
3. Database connection parameters are structured in `config/database.json`.
