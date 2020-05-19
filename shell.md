# Shell

### Heroku deploy

```bash
#!/bin/sh

# first create a heroku instance, by going to the web interface or doing heroku create on the command line
# put in Procfile:
# worker: python remindme.py

cd ..
mkdir .tmp
cp -r APPNAME/. .tmp
cd .tmp  # make .tmp in parent directory

# app specific things HERE

#############

git init
heroku git:remote -a HEROKUAPP
git add .
git commit -m "new version $(date)"
git push heroku master -f
heroku ps:scale worker=1

# clean up
cd ..
rm -rf .tmp
cd APPNAME
```

