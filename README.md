# KURU PHP Recruitment test

The test scenario is a cache warming application.
When a website uses full page caching (like Varnish Cache) there may be requirement to periodically warm cache contents.
This consists of purging cache contents for given address and visiting given address.
The following application allows for multiple users to define multiple websites and for those websites to define multiple URLs to visit.

## Prerequisites
For this task you will need a LAMPish stack.
* PHP
* MySQL
* A web server (Apache, Nginx, etc.)

Application uses:
* [composer](http://getcomposer.org)
* [PDO](http://php.net/manual/en/book.pdo.php) for MySql access
* [Silly](https://github.com/mnapoli/silly) for CLI commands
* [FastRoute](https://github.com/nikic/FastRoute) for routing
* [PHP-DI](http://php-di.org/) as dependency injection container

The following diagram shows the database schema which you will create in Task 1
![Database Scheme](doc/db.png)

## Task 1

Fork this git repository.
_Make sure to commit Your work after every completed task._
> Hint: make sure Your solutions are private, do NOT make pull requests against this repository to submit Your solutions

Clone it to your local machine into a directory of your choosing.
`git clone https://github.com/kurufootwear/kuru-dev-test.git [dest dir]

Install composer packages.
`./composer.phar install`

Create the MySQL DB schema.
`mysql -u root -e "CREATE SCHEMA kuru_dev_test DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;"`

Install and configure application by running the following command
`php console.php migrate_db`
This will promt you for DB location and credentials and create the requirted DB tables.

If you need to you can run a PHP built-in server by running following command
`php -S 0.0.0.0:8000 -t web/`
The web application will be located at http://localhost:8000.

Now modify `.gitignore` file appropriate for Your development environment.

## Task 2

The console command `php console.php warm 3` is failing because it cannot access the legacy library located in the `lib` directory.
Fix this problem.

## Task 3

Modify the application so that we can see and track time of last page visit.
This will require a database modification, changes to cache warming process and changes to pages views.
> Hint: for introducing database changes see `\Kuru\DevTest\Command\MigrateCommand`

## Task 4

On the homepage for logged in users add following information:
* Total number of pages associated with this user
* Least recently visited page
* Most recently visited page

## Task 5

Allow users to define multiple caching servers.
Each caching server has it's own unique IP address and can cache multiple websites.
You can assume that different users do not share caching servers.
This will require database modification, changes to cache warming process and changes on the frontend.
Use the partial solution available in branch `task/five`.
Use AJAX requests for saving caching server - website association.

## Task 6

As you may have noticed pages that require a logged in user are visible to all users, and those that make sense only for not logged in users (like login or registration forms) are visible to logged in users.
Introduce modifications that will fix this problem (show the login form to not logged in users on pages that require user context and impliment a 403 redirect on login and registration forms when the user is already logged in).

**When you are finished, email your name and a link to your forked repo to jim@kurufootwear.com**
