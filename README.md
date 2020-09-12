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

# DB設計

## usersテーブル
|Column|Type|Options|
|------|----|-------|
|nickname|string|null: false|
|email|string|null: false, unique: true|
|password|string|null: false|
|family_name_kanji|string|null: false|
|first_name_kanji|string|null: false|
|family_name_kana|string|null: false|
|first_name_kana|string|null: false|
|birth_year_id|integer|null: false|
|birth_month_id|integer|null: false|
|birth_day_id|integer|null: false|

### Association
- has_many :items
- has_many :perchases
- belongs_to_active_hash :birth_year
- belongs_to_active_hash :birth_month
- belongs_to_active_hash :birth_day


## Sendsテーブル
|Column|Type|Options|
|------|----|-------|
|family_name_kanji|string|null: false|
|first_name_kanji|string|null: false|
|family_name_kana|string|null: false|
|first_name_kana|string|null: false|
|perchase|references|foreign_key: true|
|postcode|string|null: false|
|prefecture_id|integer|null: false|
|city|string|null: false|
|block|string|null: false|
|building|string|-------|
|tel|string|-------|

### Association
- belongs_to :perchase
- belongs_to_active_hash :prefecture


## Itemsテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|description|text|null: false|
|price|integer|null: false|
|user|references|foreign_key: true|
|brand|references|foreign_key: true|
|category_id|integer|null: false|
|condition_id|integer|null: false|
|shipping_fee_id|integer|null: false|
|delay|integer|null: false|
|prefecture|integer|null: false|

### Association
- has_one :perchase
- has_many :images
- belongs_to :user
- belongs_to :brand
- belongs_to_active_hash :category
- belongs_to_active_hash :condition
- belongs_to_active_hash :shipping_fee
- belongs_to_active_hash :delay
- belongs_to_active_hash :prefecture

## Perchasesテーブル
|Column|Type|Options|
|------|----|-------|
|date|date|null: false|
|user|references|foreign_key: true|
|item|references|foreign_key: true|

## Association
- belongs_to :user
- belongs_to :item
- has_one :send


## Brandsテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false, unique: true|

### Association
- has_many :items


## Imagesテーブル
|Column|Type|Options|
|------|----|-------|
|body|text|null: false|
|item|references|foreign_key: true|

### Association
- belongs_to :item
