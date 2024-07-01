require 'bundler/gem_tasks'
require 'rspec/core/rake_task'
require 'rubocop/rake_task'

desc 'Build the package and publish it to rubygems.pkg.github.com'
task publish: :build do
  # Requires local setup of personal access token, see:
  # 1. https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-rubygems-registry#authenticating-with-a-personal-access-token
  system("gem push --key github --host https://rubygems.pkg.github.com/art19 " \
         "pkg/jsonapi-serializer-#{JSONAPI::Serializer::VERSION}.gem")
end

desc('Codestyle check and linter')
RuboCop::RakeTask.new('rubocop') do |task|
  task.fail_on_error = true
  task.patterns = [
    'lib/**/*.rb',
    'spec/**/*.rb'
  ]
end

RSpec::Core::RakeTask.new(:spec)
task(default: [:rubocop, :spec])
