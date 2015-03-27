# Doorkeeper::JWT

Doorkeeper JWT adds JWT token support to the Doorkeeper OAuth library.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'doorkeeper-jwt'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install doorkeeper-jwt

## Usage

In your `doorkeeper.rb` initializer add the follow to the `Doorkeeper.configure` block:

```ruby
access_token_generator "Doorkeeper::JWT"
```

Then add a `Doorkeeper::JWT.configure` block below the `Doorkeeper.configure` block to set your JWT preferences.

```ruby
Doorkeeper::JWT.configure do
  # Set the payload for the JWT token. This should contain unique information
  # about the user.
  # Defaults to a randomly generated token in a hash
  # { token: "RANDOM-TOKEN" }
  payload do
    {
      user: {
        id: 123,
        first_name: "Jane",
        last_name: "Doe",
        email: "jdoe@example.com"
      }
    }
  end

  # Set the encryption secret. This would be shared with any other applications
  # that should be able to read the payload of the token.
  # Defaults to "secret"
  secret "MY-SECRET"

  # Specify encryption type. Supports any algorithim in
  # https://github.com/progrium/ruby-jwt
  # defaults to nil
  encryption_method :hs512
end
```

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release` to create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

1. Fork it ( https://github.com/[my-github-username]/doorkeeper-jwt/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request