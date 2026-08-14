source "https://rubygems.org"

# The site is built with Jekyll 4 and deployed by .github/workflows/pages.yml,
# NOT by GitHub Pages' built-in builder. Do not swap this for the `github-pages`
# gem: it pins Jekyll 3.10, which lacks the `push` array filter that the
# semester grouping on the homepage depends on.
gem "jekyll", "~> 4.4.1"

group :jekyll_plugins do
  gem "jekyll-sitemap", "~> 1.4"
end

# Windows and JRuby do not include zoneinfo files, so bundle the tzinfo-data gem
# and associated library.
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.1", :platforms => [:mingw, :x64_mingw, :mswin]

# Lock `http_parser.rb` gem to `v0.6.x` on JRuby builds since newer versions of
# the gem do not have a Java counterpart.
gem "http_parser.rb", "~> 0.6.0", :platforms => [:jruby]
