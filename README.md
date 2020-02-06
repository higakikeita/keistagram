# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...
# users table
|Column|Type|Options|
|------|----|-------|
### Association
has_many :posts, dependent: :destroy
has_many :likes
has_many :comments
# comments table
|Column|Type|Options|
|------|----|-------|
|comment|text|
|post   |references|foreign_key: true null: false|
|user   |references|foreign_key: true null: false|
### Association
belongs_to :user
belongs_to :post

# posts table
|Column|Type|Options|
|------|----|-------|
|caption|string|
|user   |references|foreign_key: true null: false|
### Association
belongs_to :user
has_many :photos, dependent: :destroy
has_many :likes, -> { order(created_at: :desc) }, dependent: :destroy
has_many :comments, dependent: :destroy

# likes table
|Column|Type|Options|
|------|----|-------|
|post  |references  |foreign_key: true null: false|
|user  |references  |foreign_key: true null: false|
### Association
belongs_to :user
belongs_to :post
validates :user_id, uniqueness: { scope: :post_id }
# photos table
|Column|Type|Options|
|------|----|-------|
|image |string|null: false|
|post  |references|foreign_key: true null: false|

### Association
belongs_to :post
validates :image, presence: true
