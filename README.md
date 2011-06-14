# Hoptoad Server v2 for Redmine

An implementation of the Hoptoad protocol v2 for Redmine which automatically creates issues from notices submitted via Hoptoad notifiers.
Inspired by and loosely based on the [v1 Hoptoad server by Jan Schulz-Hofen](https://github.com/yeah/redmine_hoptoad_server)


## Installation

Install the hpricot gem, then install the plugin into Redmine [as usual](http://www.redmine.org/projects/redmine/wiki/Plugins).
Now go to _Administration -> Settings -> Incoming emails_ and, if neccessary, check the box _Enable WS for incoming emails_ and generate an API key. This is the key you will need in the next step to configure your notifier.


## Client-Configuration

For a Rails application, just setup the Hoptoad notifier as usual, then modify `config/initializers/hoptoad.rb` according to your needs using this template:

	HoptoadNotifier.configure do |config|
	  config.api_key = {:project => 'redmine_project_identifier',    # the identifier you specified for your project in Redmine
	                    :tracker => 'Bug',                           # the name of your desired tracker
	                    :api_key => 'redmine_api_key',               # the key you generated in the previous step
	                    :category => 'Development',                  # the name of a ticket category (optional.)
	                    :assigned_to => 'admin',                     # the login of a user the ticket should get assigned to by default (optional.)
	                    :priority => 5                               # the default priority (use id instead of name, optional.)
	                   }.to_yaml
	  config.host = 'my_redmine_host.com'                            # the hostname your Redmine runs at
	  config.port = 443                                              # the port your Redmine runs at
	  config.secure = true                                           # sends data to your server via SSL (optional.)
	end

That's it. You may run `rake hoptoad:test` to generate a test issue.
If it doesn't work, check your logs and configuration, then [submit an issue on Github](https://github.com/milgner/redmine_hoptoad_server_v2/issues)


## License

This plugin is licensed under the [Apache license 2.0](http://www.apache.org/licenses/LICENSE-2.0.html)


## Author

Written by Marcus Ilgner (mail@marcusilgner.com)

[![Flattr this](http://api.flattr.com/button/flattr-badge-large.png)](http://flattr.com/thing/307397/Hoptoad-server-plugin-for-the-Redmine-issue-tracker)