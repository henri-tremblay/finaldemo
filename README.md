# finaldemo

This example demonstrate the difference between `liquibase-hibernate4` and `liquibase-hibernate5`.

## Steps to see the errors

```bash
# Start the database (you can do that in another shell)
docker-compose -f src/main/docker/mysql.yml up &

# Use the old version
git checkout hibernate4

# This will create the original database
mvn spring-boot:run

# Get the hibernate5 version
git checkout master

# Issue #1: The checksum is considered different. The app won't start
mvn spring-boot:run

# Issue #2: The hibernate_sequence will appear in the diff
# Issue #3: The naming is different, no underscore after FK_# Issue #2: The hibernate_sequence will appear in the diff
mvn liquibase:diff
git status # to see the changelog created
```
