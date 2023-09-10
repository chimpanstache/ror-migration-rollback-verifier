# Ruby on Rails Migration Rollback Verifier

#### This script aimed for github actions, verifies that migration files are not breaking when rolled down.

It scans your commit files for migration files.  
If any, roll them down with `rake db:migrate:down`  
Then roll them back with `rake db:migrate`  
If there's no migration or the rollback has been succesful, it exits with status code 0.  
Otherwise it exits with status code 1.  

## User guide
chmod +x the script file  
In your workflow file add the following lines:  
```
- uses: actions/checkout@v3
    with:
        fetch-depth: 0
    - name: Set up Ruby
    uses: ruby/setup-ruby@v1
    with:
        bundler-cache: true
    - name: Migration Rollback Verifier
    run: |
        ./<ror_migration_rollback_verifier_path> ${{ steps.changed-files.outputs.all_changed_files }}
```
