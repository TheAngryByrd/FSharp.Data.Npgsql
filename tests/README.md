# Darren notes on setting up testing

You need to build a postgres-gis image (need v12 for compatibility with restore)

You need unix line endings on restore_dvdrental.sh or else you will get a cryptic ': No such file or directory' error building the image.  `dos2unix` will fix the endings.  git will go and break them again :(

## Running docker image 
Run `docker-compose up` in the tests directory.

This should start up and successfully restore the dvdrental database inside the docker image (copies in file then runs `pg_restore`.  If either of those steps fails you won't have a working database.

## Troubleshooting

If your tests are having trouble connecting, try connecting to db from commandline

E.g. for bash on windows

`winpty /c/Program\ Files/PostgreSQL/12/bin/psql -h 127.0.0.1 -U postgres -d dvdrental -p 32768`


## Updating test data

* Create working database
* Connect and alter schema
* Dump and rename dvdrentalnew.tar to dvdrental.tar when it looks good

`$ winpty /c/Program\ Files/PostgreSQL/12/bin/pg_dump -U postgres -h 127.0.0.1 -p 32768 --schema public -F t -f dvdrentalnew.tar dvdrental`
