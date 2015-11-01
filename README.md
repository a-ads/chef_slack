chef_slack Cookbook
===================

[![Build Status](https://travis-ci.org/chef-cookbooks/chef_slack.svg?branch=master)](https://travis-ci.org/chef-cookbooks/chef_slack)
[![Cookbook Version](https://img.shields.io/cookbook/v/chef_slack.svg)](https://supermarket.chef.io/cookbooks/chef_slack)

This cookbook sends messages to a [Slack](http://www.slack.com) chatroom using the Incoming
Webhook Integration

Requirements
------------

#### packages
- `slack-notifier` - Uses the [slack-notifier](https://github.com/stevenosloan/slack-notifier.git)
  rubygem to talk to Slack


Attributes
----------

#### slack::default
<table>
  <tr>
    <th>Key</th>
    <th>Type</th>
    <th>Description</th>
    <th>Default</th>
  </tr>
  <tr>
    <td><tt>['slack']['webhook_url']</tt></td>
    <td>String</td>
    <td>Your Incoming Webhook URL</td>
    <td><tt>nil</tt></td>
  </tr>
</table>


Custom Resource Usage
-----
In your `metadata.rb` you need to add `depends 'slack'` and add `include_recipe 'slack'` to your recipe. Passing the below will use default attributes

```ruby
slack_notify "Say Summat!"
```

```ruby
slack_notify "send_notification_message" do
  message "This is a notification message"
  webhook_url 'https://hooks.slack.com/services/XXXX/XXXXXXX/XXXXXX'
  not_if { node['im_boring'] }
end
```

```ruby
slack_notify "channel_nothing" do
  message "heres a message to kick off later"
  username 'test_user'
  channels ['foo','bar']
  webhook_url 'https://hooks.slack.com/services/XXXX/XXXXXXX/XXXXXX'
  action :nothing
end

something "talk_as_test_user_to_multiple_channels" do
  notifies :say, "slack[channel_nothing]", :immediately
end
```



License & Authors
-----------------
```
Author: Ian Henry <ihenry@chef.io>

Copyright:: 2009-2015, Chef Software, Inc

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```