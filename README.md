## users

| Column              | Type    | Options                    |
|---------------------|---------|----------------------------|
| nickname            | string  | null: false, unique: true  |
| email               | string  | null: false, unique: true  |
| encrypted_password  | string  | null: false                |

has_many :posts
has_many :comments
has_many :likes
has_one_attached :profile_image
has_many :relationships, class_name: "Relationship", foreign_key: "follower_id", dependent: :destroy
has_many :relationships, class_name: "Relationship", foreign_key: "following_id", dependent: :destroy
has_many :followers, through: :relationships, source: :following
has_many :followings, through: :relationships, source: :follower




## posts

| Column      | Type        | Options                         |
|-------------|-------------|---------------------------------|
| post        | string      | null: false                     |
| country_id  | integer     | null: false                     |
| user        | references  | null: false, foreign_key: true  |

belongs_to :user
has_many :comments
has_many :likes
has_many_attached :post_images


## comments

| Column   | Type        | Options                         |
|----------|-------------|---------------------------------|
| comment  | text        | null: false                     |
| user     | references  | null: false, foreign_key: true  |
| post     | references  | null: false, foreign_key: true  |

belongs_to :user
belongs_to :post


## likes

| Column  | Type        | Options                         |
|---------|-------------|---------------------------------|
| user    | references  | null: false, foreign_key: true  |
| post    | references  | null: false, foreign_key: true  |

belongs_to :user
belongs_to :post


## relationships

| Column        | Type        | Options                         |
|---------------|-------------|---------------------------------|
| follower_id   | references  | null: false, foreign_key: true  |
| following_id  | references  | null: false, foreign_key: true  |

  belongs_to :follower, class_name: "User"
  belongs_to :following, class_name: "User"