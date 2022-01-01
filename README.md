# fsnd_heroku_sample

1. Create a Heroku app:
```
heroku create name_of_your_app

# Example
heroku create fsnd-heroku-sample-xj
```

This returns a git url for your Heroku application, which you will need in a moment.
```
 ›   Warning: heroku update available from 7.59.0 to 7.59.2.
Creating ⬢ fsnd-heroku-sample-xj... done
https://fsnd-heroku-sample-xj.herokuapp.com/ | https://git.heroku.com/fsnd-heroku-sample-xj.git
```

2. Add git remote for Heroku to local repository

Using the git url obtained from the last step, in terminal run: 
```
git remote add heroku heroku_git_url

# Example
git remote add heroku https://git.heroku.com/fsnd-heroku-sample-xj.git
```

Note: I had to change the command to link an existing repo to the heroku app `fsnd-heroku-sample-xj` for the first time:
```
heroku git:remote -a fsnd-heroku-sample-xj
```

Which returns:
``` 
›   Warning: heroku update available from 7.59.0 to 7.59.2.
set git remote heroku to https://git.heroku.com/fsnd-heroku-sample-xj.git
```

3. Add postgresql add on for our database

Heroku has an addon for apps for a postgresql database instance. Run this code in order to create your database and connect it to your application: 
```
heroku addons:create heroku-postgresql:hobby-dev --app name_of_your_application

# Example
heroku addons:create heroku-postgresql:hobby-dev --app fsnd-heroku-sample-xj
```

A sample output:
```
 ›   Warning: heroku update available from 7.59.0 to 7.59.2.
Creating heroku-postgresql:hobby-dev on ⬢ fsnd-heroku-sample-xj... free
Database has been created and is available
 ! This database is empty. If upgrading, you can transfer
 ! data from another database with pg:copy
Created postgresql-polished-47879 as DATABASE_URL
Use heroku addons:docs heroku-postgresql to view documentation
```

Breaking down the heroku-postgresql:hobby-dev section of this command, heroku-postgresql is the name of the addon. hobby-dev on the other hand specifies the tier of the addon, in this case the free version which has a limit on the amount of data it will store, albeit fairly high.

Run `heroku config --app name_of_your_application` in order to check your configuration variables in Heroku. You will see DATABASE_URL and the URL of the database you just created.
```
heroku config --app name_of_your_application

# Example
heroku config --app fsnd-heroku-sample-xj
```

A sample output:
```
 ›   Warning: heroku update available from 7.59.0 to 7.59.2.
=== fsnd-heroku-sample-xj Config Vars
DATABASE_URL: postgres://hsochozkgbdfbp:75815ee36ad37e413842d6a998d9502531a5508303fb4498ca14b4b4e34e65ef@ec2-3-212-172-25.compute-1.amazonaws.com:5432/d86i8rkve1ff2h
```

4. Fix our configurations in Heroku

In the browser, go to your Heroku Dashboard and access your application's settings. Reveal your config variables and start adding all the required environment variables for your project. For the purposes of the sample project, just add one additional one - ‘EXCITED’ and set it to true or false in all lowercase. 

5. Commit changes and push it!
```
git add .
git commit -am "make it better"
git push heroku master
```