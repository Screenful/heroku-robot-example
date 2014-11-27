heroku-robot-example
====================

An example project that shows how to run Robot Framework tests on Heroku

## Setting up

Clone the content of this repository to your Heroku app's repository.

Configure your Heroku app to use an external buildpack.

`heroku config:add BUILDPACK_URL=http://hello.heroku.com/e/36622/oku-heroku-buildpack-multi-git/2rc718/432677817`

This allows you to use separate buildpacks for running your app (==
Robot Framework test execution). The used builpacks are listed in the
'.buildpacks' file.

Push the new files to your Heroku app repository. Heroku should start
importing the buildpacks and building your project.

Now you can run your first Robot Framework test case from Heroku with:

`heroku run tests`

### Setting up Amazon S3 uploads

If you want the log file from your test to be uploaded to your Amazon S3 bucket just set the S3_URL env var. The URL format is 

`http://<ACCESS_KEY>:<SECRET_KEY>@<END_POINT>/<BUCKET_NAME>`

For example:

`heroku config:set S3_URL=http://MAXERTHTHBSLAKBQ:FWw2rTwer4598FsDfGoiuhrt56werRcOq-e@s3-eu-west-1.amazonaws.com/my-test-logs`

## File explanation

* bin/test 
  
  Script to run the tests. Sets paths for Phantomjs and possible Robot
  libraries. Calls Robot with phantomjs as the browser to run the
  default test case from RobotTests.

* RobotTests 
  
  Example Robot Framework test project. Use this as a starting point
  for your first test.

* requirements.txt 
  
  Required by Heroku. This defines the necessary Python libraries
  required by your Heroku app. Specifically Robot Framework and
  Selenium2 libraried needed for running web tests with Robot
  Framework.

  You'll probably want to at least update the versions of these for
  you project.

* Procfile 
  
  Defines a Heroku process type, in this case the tests to run using
  Robot Framework.

* .buildpacks
  
  Which buildpacks need to be use to run the tests with Robot
  Framework. Currently Phantomjs and Python.

## Authors

Original example created by Niko Cankar, S3 upload contributed by Tuomas Tammi.
