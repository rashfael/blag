{spawn} = require 'child_process'
os = require 'os'
express = require 'express'
Metalsmith = require 'metalsmith'

markdown = require 'metalsmith-markdown'
templates = require 'metalsmith-templates'
watch = require 'metalsmith-watch'
collections = require 'metalsmith-collections'
permalinks  = require 'metalsmith-permalinks'

cmd = (name) ->
	if os.platform() is 'win32' then name + '.cmd' else name

npm = cmd 'npm'

metalsmith = ->
	Metalsmith(__dirname)
	.use(watch({livereload:true}))
	.use(collections())
	.use(permalinks())
	.use(markdown())
	.use(templates('jade'))
	.build()

serve = ->
	app = express()
	app.use express.static __dirname + '/build'
	app.listen 8000, ->
		console.log 'listening on 8000'

task 'install', 'Install node.js packages', ->
	spawn npm, ['install'], {cwd: '.', stdio: 'inherit'}

task 'update', 'Update node.js packages', ->
	spawn npm, ['update'], {cwd: '.', stdio: 'inherit'}
	
task 'watch', 'Watch brunch project', ->
	metalsmith()
	serve()