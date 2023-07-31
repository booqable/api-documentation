# Booqable API Documentation

This repository contains the source for the Booqable API documentation

### Warning: Our API is still in Beta and we might introduce non-backwards compatible changes in the future.

## Getting Started

### Prerequisites

You're going to need:

* **Linux or OS X** — Windows may work, but is unsupported.
* Ruby, version 2.3.1 or newer
* Bundler — If Ruby is already installed, but the bundle command doesn't work, just run gem install bundler in a terminal.

### Getting Set Up
1. Clone this repository
2. `cd api-documentation`
3. Initialize and start Slate. You can either do this locally, or with Vagrant:

```shell
# either run this to run locally
asdf install
bundle install
bundle exec middleman server

# OR run this to run with vagrant
vagrant up
```

You can now see the docs at http://localhost:4567. Whoa! That was fast!

## Built With
 [Slate](https://github.com/lord/slate) - API docs generator

## Contributing

The API is going to be a very important part of our eco system. We've designed the docs in a way every developer is able to contribute to our API. If you find a bug or you have a great suggestion open an issue or pull request.
