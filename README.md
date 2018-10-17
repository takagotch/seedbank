### seedbank
---
https://github.com/james2m/seedbank



```
rake db:setup

rake db:seed
rake db:seed:bar
rake db:seed:common
rake db:seed:development
rake db:seed:development:users
rake db:seed:original

rake db:seed

```
```
db/seeds/
  bar.seeds.rb
  devlopment/
    users.seeds.rb
  foo.seeds.rb

```
```ruby
RAILS_ENV=production rake db:seed
gem "seedbank"
gem "seedbank", '~> 0.2.1'

require 'seedbank'
Seedbank.load_tasks if defined?(Seedbank)

Company.find_or_create_by_name('Hatch', :url => 'http://thisishatch.co.uk')
# db/seeds/users.seeds.rb
after :companies do
  company = Company.find_by_name('Hatch')
  company.users.create(:first_name => 'James', :last_name => 'McCarthy')
end
# db/seeds/projects.seeds.rb
after :companies do
  company = Company.find_by_name('Hatch')
  company.projects.create(:title => 'Seedbank')
end
# db/seeds/tasks.seeds.rb
after :projects, :users do
  project = Project.find_by_name('Seedbank')
  user = User.find_by_first_name_and_last_name('James', 'McCarthy')
  project.tasks.create(:owner => user, :title => 'Document seed dependencies in the README.md')
end
# db/seeds/development/users.seeds.rb
after "development:companies" do
  company = Company.find_by_name('Hatch')
  company.users.create(:first_name => 'James', :last_name => 'McCarthy')
end
# db/seeds/support.rb
module Support
  def notify(filename)
    puts "Seeding: #{filename}"
  end
end
# db/seeds/users.seeds.rb
after :common do
  notify(__FILE__)
end




```

```

```
