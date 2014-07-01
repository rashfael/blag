{spawn} = require 'child_process'
os = require 'os'
express = require 'express'
Metalsmith = require 'metalsmith'
markdown = require 'metalsmith-markdown'
templates = require 'metalsmith-templates'
watch = require 'metalsmith-watch'

cmd = (name) ->
	if os.platform() is 'win32' then name + '.cmd' else name

npm = cmd 'npm'

metalsmith = ->
	Metalsmith(__dirname)
	.use(watch({livereload:true}))
	.use(markdown())
	.use(templates('jade'))
	.build()

serve = ->
	app = express()
	app.use express.static __dirname + '/build'
	app.listen 8000

task 'install', 'Install node.js packages', ->
	spawn npm, ['install'], {cwd: '.', stdio: 'inherit'}

task 'update', 'Update node.js packages', ->
	spawn npm, ['update'], {cwd: '.', stdio: 'inherit'}
	
task 'build', 'Build brunch project', ->
	metalsmith()
	serve()

task 'watch', 'Watch brunch project', ->
	brunch = spawn brunch, ['watch', '--server'], {cwd: '.', stdio: 'inherit'}
	brunch.on 'exit', (status) -> process.exit(status)