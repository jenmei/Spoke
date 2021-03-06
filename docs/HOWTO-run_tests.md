There are current two ways to run tests, using either PostgreSQL or SQLite.

## PostgreSQL Testing (default, closer to most prod environments)

1) Install PostgreSQL - [Tips to installing Postgres](https://www.codementor.io/engineerapart/getting-started-with-postgresql-on-mac-osx-are8jcopb)
2) In PostgreSQL, create a database and user named "spoke_test":
```
CREATE DATABASE spoke_test;
CREATE USER spoke_test WITH PASSWORD 'spoke_test';
GRANT ALL PRIVILEGES ON DATABASE spoke_test TO spoke_test;
```
3) Run `yarn test`

## SQLite Testing (simpler)

1) Run `yarn run test-sqlite`
  
## Test Redis Cache

Redis is used for caching and is separate from the backend DB so can be used with sqlite *or* postgres. Redis cache testing defaults to postgres and functions like an 'addon' to the DB for improved speed/scalability.

1) Run `yarn test-rediscache`

## End-To-End (Interactive Browser) Testing

1. Remember to set `NODE_ENV=dev` 
2. **Start DB** and **Start Spoke Server** as described in the [Getting Started](
https://github.com/MoveOnOrg/Spoke/blob/main/README.md#getting-started) section. 
1. Install browser driver(s)
    
    * Installing chromedriver on MacOS
        ```
        brew tap homebrew/cask
        brew cask install chromedriver
        ```
    * References
        * [Selenium HQ - JavaScript Docs](http://seleniumhq.github.io/selenium/docs/api/javascript/)
        * [Homebrew - Casks - chromedriver](https://github.com/Homebrew/homebrew-cask/blob/master/Casks/chromedriver.rb)
1. Running tests...
    * ... using your local browser
      ```
      yarn run test-e2e
      ```
    * ... individually
      ```
      yarn run test-e2e <test name>
      ```
    * ... using Sauce Labs browser with your local host
      
      **Note:** You must first setup [Sauce Labs](https://github.com/MoveOnOrg/Spoke/blob/main/docs/EXPLANATION-end-to-end-tests.md#saucelabs)
      ```
      export SAUCE_USERNAME=<Sauce Labs user name>
      export SAUCE_ACCESS_KEY=<Sauce Labs access key>
      yarn run test-e2e <optional test name> --saucelabs
      ```