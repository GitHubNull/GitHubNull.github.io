source 'https://rubygems.org'

require 'json'
require 'open-uri'
versions = JSON.parse(open('https://pages.github.com/versions.json').read)

gem 'rouge'
gem 'jekyll'
gem 'jemoji'
gem 'github-pages', versions['github-pages']
