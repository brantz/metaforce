Metaforce
=========
Metaforce is a Ruby gem for interecting with the [Salesforce Metadata API](http://www.salesforce.com/us/developer/docs/api_meta/index.htm).
The goal of this project is to make the [Migration Tool](http://www.salesforce.com/us/developer/docs/apexcode/Content/apex_deploying_ant.htm) obsolete, favoring Rake over Ant.

Usage
-----

``` ruby
client = Metaforce::Metadata::Client.new :username => 'username',
    :password => 'password',
    :security_token => 'security token')

client.describe
# => { :metadata_objects => [{ :child_xml_names => "CustomLabel", :directory_name => "labels" ... }

client.list(:type => "CustomObject")
# => [{ :created_by_id => "005U0000000EGpcIAG", :created_by_name => "Eric Holmes", ... }]

deployment = client.deploy(File.expand_path("../src"))
# => #<Transaction:0x00000102779bf8 id="04sU0000000WNWoIAO" type=:deploy> 

deployment.done?
# => false

deployment.wait_until_done
deployment.result
# => { :id => "04sU0000000WNWoIAO", :messages => [{ :changed => true ... :success => true }
```
