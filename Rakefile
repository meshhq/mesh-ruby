require 'rest-client'
require 'json'

class User
  attr_accessor :first_name
  attr_accessor :last_name
  attr_accessor :email
  attr_accessor :title
  attr_accessor :organization_name
  attr_accessor :external_id
  attr_accessor :custom_fields

  def to_json
    {
      :first_name => @first_name,
      :last_name => @last_name,
      :email => @email,
      :title => @title,
      :organization_name => @organization_name,
      :external_id => @external_id,
      :custom_fields => @custom_fields,
    }.to_json
  end
end

class Organization
  attr_accessor :name
  attr_accessor :website
  attr_accessor :industry
  attr_accessor :size
  attr_accessor :annual_revenue
  attr_accessor :custom_fields

  def to_json
    {
      :name => @name,
      :website => @website,
      :industry => @industry,
      :size => @size,
      :annual_revenue => @annual_revenue,
      :custom_fields => @custom_fields,
    }.to_json
  end
end

MESH_APP_ID = ""
MESH_AUTH_TOKEN = ""

namespace :new do
  desc "Creates a new organization with the Mesh REST API"
  task :organization do
    organization = Organization.new
    organization.name = "Mesh Data, Inc."
    organization.website = "www.meshdata.io"

    url = "https://api.meshdata.io/apps/#{MESH_APP_ID}/organizations"
    response = RestClient.post url, organization.to_json, :content_type => :json, :accept => :json, :authorization => "bearer #{MESH_AUTH_TOKEN}"
    json = JSON.parse(response)
    puts JSON.pretty_generate(json)
  end

  desc "Creates a new user with the Mesh REST API"
  task :user do
    user = User.new
    user.first_name = "Kevin"
    user.last_name = "Coleman"
    user.email = "kevin2@meshdata.io"
    user.title = "Engineer"
    user.custom_fields = {
      "salesforce" => {
        "Department" => "Engineering",
        "Newsletter_Subscriber" => true,
        "Initial_Interest" => true,
        "Has_Opted_Out_Of_Email" => true,
        "Expires" => Date.new(2016,6,14),
        "Plan" => "Growth",
        "Logins" => 1,
        "Feed_View" => 1,
        "Profile_Views" => 1,
        "Skill_Views" => 1,
        "Test_Views" => 1,
        "Beastmode_Views" => 1,
        "Skills_To_Feed" => 1,
        "Skills_In_Feed" => 1,
        "Tests_Submitted" => 1,
        "Tests_Passed" => 1,
        "Beastmodes_Submitted" => 1,
        "Beastmodes_Passes" => 1,
        "Days_Since_Last_Login" => 1,
      }
    }
    url = "https://api.meshdata.io/apps/#{MESH_APP_ID}/users"
    response = RestClient.post url, user.to_json, :content_type => :json, :accept => :json, :authorization => "bearer #{MESH_AUTH_TOKEN}"
    json = JSON.parse(response)
    puts JSON.pretty_generate(json)
  end
end

namespace :update do
  desc "Updates an exsiting user with the Mesh REST API"
  task :user do
    user = User.new
    user.email = "new@meshdata.io"

    url = "https://api.meshdata.io/apps/#{MESH_APP_ID}/users/#{user_id}"
    RestClient.put url, user.to_json, :content_type => :json, :accept => :json, :authorization => "bearer #{MESH_AUTH_TOKEN}"
  end
end
