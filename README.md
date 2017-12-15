# Basic Mongoose Service Provider for Adonis 4.0

> Basically from the old [npm package](https://www.npmjs.com/package/adonis-mongoose) used for Adonis 3.^

### Installation

* Ultra instinct mode on
```curl
$ npm install adonis-4-mongoose --save
```

* Update the `.env` file with your mongo credentials.

```env
MONGO_HOST=localhost
MONGO_PORT=27017
MONGO_USER=yoursupersaiyanusername
MONGO_PASS=yoursuperawesomepass
MONGO_DATABASE=yourultrainstinctdb
```

* Add config file `config/mongo.js` to your project

```javascript

const Env = use('Env')

module.exports = {
  host: Env.get('MONGO_HOST', 'localhost'),
  port: Env.get('MONGO_PORT', '27017'),
  user: Env.get('MONGO_USER', ''),
  pass: Env.get('MONGO_PASS', ''),
  db: Env.get('MONGO_DATABASE', '')
}

```


* Update `start/app.js` add the mongoose service provider

```javascript

const providers = [
  ...
  'adonis-4-mongoose/provider/Mongoose'
]

const aliases = {
  ...
  Mongoose: 'Adonis/Addons/AdonisMongoose'
}

```

### Basic Usage

Add/Update your user model `app/Models/User.js`

```javascript

'use strict'

const mongoose = use('Mongoose')
const ObjectId = mongoose.Schema.Types.ObjectId
const Mixed = mongoose.Schema.Types.Mixed

let userSchema = mongoose.Schema({
  firstName: { type: String, default: '' },
  lastName: { type: String, default: '' },
  dob: { type: Date },
  email: { type: String, default: '' },
  mobile: { type: String, default: '' },
  password: { type: String, default: '' },
  isActive: { type: Boolean, default: true },
  likes: { type: Mixed, default: {} },
  interests: [{ type: Mixed, default: {} }],
}, {
  timestamps: true
})

module.exports = mongoose.model('User', userSchema)


```

Use basic mongoose query `app/Controllers/Http/UserController.js`

```javascript

'use strict'

const User = use('App/Models/User')

class UserController {

  async index ({ response }) {
    let users = await User.find({})
    response.json({ users })
  }

}


module.exports = UserController

```
