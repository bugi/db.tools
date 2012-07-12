# A collection of tools for command-line mysql db administration.

## Recommended usage:

Drop the db.tools directory somewhere.  Then either put this directory in your PATH or symlink each script into directory that is in your path.  I personally use the latter approach.


## Usage:

### db -	a command-line tool to make working with one or more mysql instances easier.

- It supports tab completion.

- examples:

	* list the schemata in the "foo" mysql instance
		`db foo ls`

	* list the mysql instances it finds on the current host
		`db tag`

	* list available commands in context
		`db` *&lt;space&gt;* *&lt;tab&gt;*

	* list the schemata in foo that start with a "b"
		`db foo cli b`*&lt;tab&gt;*

	* start a mysql command-line instance in the schema *bar*
		`db foo cli bar`

	* show table defn of *bar.acct*
		`db foo ls bar acct`

	* show code for setup of credentials for accessing the db as root
		`db auth-set root`

	* setup credentials for accessing the db as root
		`eval "$( db auth-set root )"`


### setup the tools:

	cd /baz/bin
	git clone git://github.com/bugi/db.tools.git
	ln -s db.tools/db .
	cd db.tools/db.conf
	cp -a default this
	cp -p pool/local.params this/
	cat this/setup	# edit to your taste
	cat this/local.params	# edit to your taste
	. /baz/db.tools/db.conf/pool/completion_dbtool	# add to your bashrc

### setup mysql instance for use with tool:

For the typical single-instance install, copy the db.tools/example/dbtool\_conf file into your mysql data directory.  Edit this/local.params to make the tool find your mysql data directory.

### security:

Although this tool tries not to expose your credentials, it is best not to use this tool in other than a trusted environment.

It is assumed that the unix user you run as can read the mysql data dir and the dbtool\_conf file.  It need not be able to read the schema directories.  To make this secure, use unix groups and/or make your machine difficult to compromise.

### customization:

The tool is decomposed into modules on purpose.  The authentication system is especially customizable.

If you come up with a better auth system, please share...

### More/better documentation welcome.
