# HOW TO DUMP AND COPY DATABASE
1. Create a new Database: `mysqladmin -u root createdatabase lportal73`
2. Dump the current Database: `mysqldump -u root lportal > dump73.sql`
3. Import the dumped file to the new Database: `mysql -u root lportal73 < lportal73.sql`

# RUNNING UPGRADE
1. Go to `../bundles/liferay-portal/tools/portal-tools-db-upgrade-client`
2. Run `./db_upgrade`

# RUNNING UPGRADE AGAIN WITHOUT ANT ALL
1. Go to `../bundles/liferay-portal/tools/portal-tools-db-upgrade-client`
2. Remove  `portal-upgrade-database.properties and portal-upgrade-ext.properties`
3. Run `./db_upgrade`

# DEBUGGING UPGRADE
1. Go to `../bundles/liferay-portal/tools/portal-tools-db-upgrade-client`
2. Run `./db_upgrade.sh --debug`

# RUNNING UNIT TESTS:
- Running tests: `gw test`
- Debugging tests: `gw test --tests com.liferay.data.engine... --debug-jvm`

# RUNNING INTEGRATION TESTS
- Running tests: `gw testIntegration`
- Debbuging tests: `gw testIntegration --tests com.liferay.data.engine...`

# RUNNING FUNCTIONAL POSHI TESTS:
Run: `ant -f build-test.xml run-selenium-test -Dtest.class=TestClass#TestName`

# DEPLOYING MODIFIED MODULES
 - `gw deploy`
 - `gw deploy -a`
 - `gw clean deploy`
 - `gw deploy -a`

# ACCESS TO GITHUB CLI MANUAL:
- https://cli.github.com/manual/

# STEPS TO SEND A PULL REQUEST
1. Verify the format source
	1. Run gw formatsource
    2. Fix every wrong source
2. If everything is correct
    1. Run: `git add .`
3. Verify if the branch's name is correct
4. Run: `git commit -m "LPS-xxxxxx message"`
5. Run: `git pull --rebase upstream master`
6. Then `gh pr create -R liferay-data-engine/liferay-portal -t "pr's title" -b "pr's description"`

# CODE REVIEW
- Pull PR branch for local review: `gh pr checkout prURL`
- Approve PR: `gh ph review prURL -a`
- Leave a comment: `gh ph review prURL --comment -b "comment"`

# SOME GIT COMMANDS
1. `git pull --rebase upstream master`
2. `git clean -f`
3. `git checkout -b "branch name"`
4. `git stash`
5. `git stash list`
6. `git stash apply`
7. `git stash apply stash@{2}`
8. `git stash drop stash@{2}`
9. `git commit --amend -m "New commit message"`

# CI GITHUB
- ci:test:sf
- ci:test:relevant
- ci:forward

# BRANCH FETCHING
1. Add remote pointing to "USERNAME" repository
    1. `git remote add "username" https://github.com/username/liferay-portal.git` 
2. Run: `fetch pull/pullRequestID/head:nomeBranchLocal`
3. Run: `git cherry-pick commitIdentfierˆ..commitIdentifier`
   1. Fetching branch: `git fetch git@github.com:rodrigopaulino/liferay-portal.git --no-tags LPS-125463:Wip-Paulino`

# JUNTAR COMMITS
Links where I learned from:
- https://imasters.com.br/desenvolvimento/git-como-juntar-diversos-commits-em-apenas-um
- https://blog.psantos.dev/git-como-juntar-varios-commits-em-apenas-um/

Steps:
1. Run: `git rebase -i HEAD~3`
2. Run: change "pick" to "squash"
3. Run: write the commit message