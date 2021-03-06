# Bundler

## Details

- `bundle install`: Will install to your gem path by default
- `bundle install --deployment`: Will install gems locally

## Standalone

1. Run `bundle init` to create a `Gemfile`
2. Add `.bundle` to `.gitignore`
3. Edit the `Gemfile` to add required gems
4. Run `bundle install --standalone`
5. Add `require_relative 'bundle/bundler/setup'` to the script

### Updating Gems

	bundle update <gem name> --full-index
	bundle install --standalone
	bundle update
	bundle clean
	bundle install --standalone

Note the second `bundle install --standalone` is necessary to update the `bundle/bundler/setup` to point to the new version of the gem.

### Troubleshooting

If a gem won't update, the following can be tried:

1. Specify the gem: `bundle update repla`
2. Use the `--full-index` option: `bundle update repla --full-index`

## Changing the Ruby Version

1. Add `ruby '2.0.0'` to the `Gemfile`
2. Delete the `.bundle` directory
3. Delete the `bundle` directory
4. Delete the `Gemfile.lock` file
4. Run `bundle install --standalone`

## `git` in Gemfile

To point to a development version of a gem:

	gem 'repla', github: 'repla-app/repla-ruby', branch: 'catalina'

Then the following will add the gem and remove the previous version:

	bundle update # Install them gem
	bundle clean # Delete the old version of the gem
	bundle install --standalone # Point the `bundle/bundler/setup` at the gem

### Adding to `git`

Since Bundler checkouts the gem from git, if you then try to add the gem to git (e.g., with `git add .`), the add will fail with a message about recursively adding git repositories ("You've added another git repository inside your current repository."). In order to add it, you'll need to use `git add <full path to repository>/`, e.g.:

	git add Contents/Resources/bundle/ruby/2.4.0/bundler/gems/repla-ruby-4992e5e09082/

Note that the trailing slash is important.
