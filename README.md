 curl -s https://api.github.com/orgs/wp-cli/repos?per_page=100 | jq -r '.[].cldone_url' | while read url; do
  archive_status=$(curl -s $url | jq -r '.archived');   if [[ "$archive_status" != "true" ]]; then     git clone "$url";   fi; done
  
  
  
  
  
  How do i set up the development environment for wp-cli in wp-cli-dev? 
ChatGPT said:

To set up the development environment for WP-CLI (specifically wp-cli-dev), follow these steps:
1. Install Dependencies

You'll need to have a few dependencies installed before you can begin developing WP-CLI.
a. PHP

WP-CLI is a command-line interface for WordPress, so it requires PHP. You can check if you have PHP installed using:

php -v

If PHP is not installed, you can install it using your system's package manager. For example:

    On Ubuntu/Debian:

sudo apt install php-cli php-curl php-mbstring php-xml php-zip

On macOS (with Homebrew):

    brew install php

<<<<<<< Updated upstream
Before you can proceed further, you'll need to make sure you have [Composer](https://getcomposer.org/), PHP, and a functioning MySQL or MariaDB server on your local machine.
=======
b. Composer
>>>>>>> Stashed changes

WP-CLI uses Composer to manage PHP dependencies, so you'll need to have Composer installed. You can check if Composer is installed using:

composer --version

If Composer is not installed, you can install it globally using:

curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer

c. Git

Git is necessary for pulling code from WP-CLI’s GitHub repository and for managing versions. Verify if you have Git installed:

git --version

If Git is not installed, you can install it using:

    On Ubuntu/Debian:

sudo apt install git

On macOS:

    brew install git

2. Clone the WP-CLI Repository

Clone the WP-CLI repository to your local machine. Choose a directory where you want to keep your WP-CLI development environment and clone the wp-cli repository.

git clone https://github.com/wp-cli/wp-cli.git
cd wp-cli

3. Set Up WP-CLI Development Environment
a. Install Development Dependencies

WP-CLI requires some development dependencies that are defined in the composer.json file. Install them using Composer:

composer install

b. Install Development Tools

WP-CLI includes various tools for testing, linting, and other development tasks. To install these tools, run:

composer install --dev

4. Configure the Development Environment

WP-CLI's development environment relies on some configuration files. You'll likely want to make sure the following files exist in your local repo:

    wp-cli.yml
    A YAML configuration file where you can specify default settings for WP-CLI commands (if needed).

    wp-config.php
    This is the typical WordPress configuration file, which you may need to create or adjust, especially if you plan to test WP-CLI commands against a local WordPress instance.

Example: Creating a Basic wp-config.php for Local Development

You may need to set up a basic WordPress environment for testing WP-CLI. Here’s a simplified example for your wp-config.php:

<?php
define( 'DB_NAME', 'wordpress' );
define( 'DB_USER', 'root' );
define( 'DB_PASSWORD', '' );
define( 'DB_HOST', 'localhost' );

define( 'WP_DEBUG', true );
define( 'WP_HOME', 'http://localhost' );
define( 'WP_SITEURL', 'http://localhost' );

5. Test Your Setup

Now that everything is set up, you can run WP-CLI commands to verify that it works. Try running:

php bin/wp --info

This command should show you information about your WP-CLI installation. If everything is set up correctly, you'll see detailed output including the version of WP-CLI, PHP, and system paths.
6. Start Developing

Now that the development environment is ready, you can start developing WP-CLI commands or contributing to the project. If you're developing a custom command or adding functionality, follow these steps:

    Write a Custom Command

        Create a PHP file in the php/commands directory.

        Define a class that extends WP_CLI_Command and define your command functionality.

    Test Your Command

        Use bin/wp to run your custom commands.

        Test your code locally with a WordPress environment set up.

7. Optional: Set Up Automated Testing

WP-CLI includes automated tests, and it's a good practice to write and run tests as you develop. To set up PHPUnit for testing:

    Install PHPUnit globally or through Composer.

    Run the test suite:

    composer run test







