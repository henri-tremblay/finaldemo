# finaldemo

This example demonstrate the difference between `liquibase-hibernate4` and `liquibase-hibernate5`.

See https://github.com/liquibase/liquibase-hibernate/issues/96.

## Evolution

### Issue #1

Liquibase doesn't consider blank lines in CSV anymore in the checksum. This includes the final
new line. To test is, I've removed than from the hibernate 4 and 5 versions.

So the application will now start normally. But of course, I'm rewriting history here. Anyone
who already have done a load data in database will still have the problem. But it is a liquibase
backward compatibility issue.

# Issu
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

# Issue #1: The checksum is considered different. The app won't start (now fixed)
mvn spring-boot:run

# Issue #2: The hibernate_sequence will appear in the diff (now fixed)
# Issue #3: The naming is different, no underscore after FK
mvn liquibase:diff
git status # to see the changelog created
```
