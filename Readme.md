*This repository is a mirror of the [component](http://component.io) module [timoxley/async-compose](http://github.com/timoxley/async-compose). It has been modified to work with NPM+Browserify. You can install it using the command `npm install npmcomponent/timoxley-async-compose`. Please do not open issues or send pull requests against this repo. If you have issues with this repo, report it to [npmcomponent](https://github.com/airportyh/npmcomponent).*
# async-compose

  Compose a series of async functions together to manipulate an object.

	Similar to an async reduce function, but each iteration pops a
	function from a stack of transformations.

## Installation

    $ component install timoxley/async-compose

## Example

```js
var compose = require('async-compose')
var request = require('visionmedia-superagent')

function getInfo(user, next) {
	request
	.get('https://api.github.com/users/' + user.name)
	.end(function(res) {
		user.hireable = res.body.hireable
		user.avatar_url = res.body.avatar_url
		next(null, user)
	})
}

function getOrgs(user, next) {
	request
	.get('https://api.github.com/users/'+user.name+'/orgs')
	.end(function(res) {
		user.orgs = res.body
		next(null, user)
	})
}

var loadInfo = compose([getInfo, getOrgs])

loadInfo({name: 'timoxley'}, function(err, user) {
	console.log('User details: %o', user)
})

```

## License

MIT
