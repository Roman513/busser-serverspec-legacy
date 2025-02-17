# <a name="title"></a> Busser::RunnerPlugin::Serverspeclegacy

[![Gem Version](https://badge.fury.io/rb/busser-serverspeclegacy.svg)](http://rubygems.org/gems/busser-serverspeclegacy) [![Build Status](https://secure.travis-ci.org/test-kitchen/busser-serverspeclegacy.svg?branch=master)](https://travis-ci.org/test-kitchen/busser-serverspeclegacy)

A Busser runner plugin for Serverspec
This is a FORK for copatinibility with Chef 12 and Ruby 2.3. Rename you `test/integration/*/serverspec` to `test/integration/*/serverspeclegacy` to use it.

```bash
ls -d1 test/integration/*/serverspec | xargs -I{} mv {}{,legacy}
```

The only difference with original gem is pinned `install_gem('bundler', '~> 1.16.1')` in postinstall, credits to [etherops](https://github.com/etherops), see the [comment](https://github.com/test-kitchen/busser-serverspec/issues/55#issuecomment-468440943)

## Status

This software project is no longer under active development as it has no active maintainers. The software may continue to work for some or all use cases, but issues filed in GitHub will most likely not be triaged. If a new maintainer is interested in working on this project please come chat with us in #test-kitchen on Chef Community Slack.

## <a name="installation"></a> Installation and Setup

Please read the Busser [plugin usage][plugin_usage] page for more details.

## <a name="usage"></a> Usage

Please put test files into [COOKBOOK]/test/integration/[SUITES]/serverspeclegacy/

```cookbook
`-- test
    `-- integration
        `-- default
            `-- serverspeclegacy
                |-- Gemfile
                |-- localhost
                |   `-- httpd_spec.rb
                `-- spec_helper.rb
```

`Gemfile` is optional. You can specify installing Serverspec version and install gems you need.

## <a name="note"></a> Note

### <a name="spec"></a> File Matching

Globbing pattern to match files is `"serverspeclegacy/*/*_spec.rb"`.
You need to use `"_spec.rb"` (underscore), not `"-spec.rb"` (minus).

### <a name="serverspec1"></a> Specify Serverspec version

If you have to specify Serverspec version, you can use Gemfile. Example Gemfile:

```Gemfile
source 'https://rubygems.org'
gem 'serverspec', '< 2.0'
```

### <a name="backend"></a> Serverspec backend

It runs on a target server for testing after ssh log in it.
So you need to specify `set :backend, :exec` not `set :backend, :ssh` (Serverspec v2).
If you use Serverspec v1, you need to specify `include SpecInfra::Helper::Exec` not `include SpecInfra::Helper::Ssh`.


## <a name="development"></a> Development

* Source hosted at [GitHub][repo]
* Report issues/questions/feature requests on [GitHub Issues][issues]

Pull requests are very welcome! Make sure your patches are well tested.
Ideally create a topic branch for every separate change you make. For
example:

1. Fork the repo
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## <a name="authors"></a> Authors

Created and maintained by [HIGUCHI Daisuke][author] (<d-higuchi@creationline.com>)

## <a name="license"></a> License

Apache 2.0 (see [LICENSE][license])


[author]:           https://github.com/cl-lab-k
[issues]:           https://github.com/test-kitchen/busser-serverspec/issues
[license]:          https://github.com/test-kitchen/busser-serverspec/blob/master/LICENSE
[repo]:             https://github.com/test-kitchen/busser-serverspec
[plugin_usage]:     http://docs.kitchen-ci.org/busser/plugin-usage
