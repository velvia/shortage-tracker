# shortage-tracker

This is a project of OSINThk.

## Setup

Works with [`rbenv`](https://github.com/rbenv/rbenv#homebrew-on-macos). May work with `rvm`.

An approximate macOS setup from basics:

```sh
brew install git rbenv postgres postgis redis

brew services start postgresql
brew services start redis

rbenv init
rbenv install 2.5.1
gem install bundler rails

git clone git@github.com:OSINThk/shortage-tracker.git
cd shortage-tracker
bundle install

rake db:create && rake db:migrate

rails s
```

Sample request: `http://localhost:3000/maptest?lat=114.029&lon=22.344&dist=1500&since=2020-01-01`

Anything that you find incomplete in the setup, please help us document!

## Contributing

Join the [Telegram group chat](https://t.me/joinchat/Aig7CRa2KapdIcMJX21--A) to get started. There you can keep up with what is happening and who is doing what. You may lay claim to individual tasks from the below TODO list.

Once we have more than one regular contributor we will use a GitHub PR workflow to organize getting work into the application.

## TODO

This is a list of many of the remaining steps to get this application into a shippable state:

### Filtered Data Bugfix

If the filtered set increases in scope (for example, becomes unfiltered after being filtered for all previous requests) all previous cursor data loads need to be adjusted for that condition change.

In other words, they need to be run with the more-permissive filter to explicitly re-add filtered out values. For example:

1. `~2020-02-04T16:22:27~114.1,22.5,114.2,22.6~7 => 719a480`
2. `719a480~2020-02-04T16:23:52~114.1,22.5,114.2,22.6~" => 79dda18`

1. Loaded reports if and only if they contained product 7.
2. Region didn't change, should get only new reports and reports matching query 1 that *did not* contain product 7.

Currently Step 2 will only get new reports; it will not expand the scope of previous queries.

### Frontend

- [ ] Report#new/Report#edit: populate coordinates via location services or map selection.

### v1 Followup

- [ ] :omniauthable
- [ ] Internationalization/Localization.
- [ ] Fix tests now that pundit is in place.
- [ ] Design for each page (mobile device focused)
- [ ] Clustering of data on the server.
- [ ] Implement CI via GitHub Actions.
- [ ] Photo upload.
- [ ] Product taxonomy.
