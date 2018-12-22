#mysql备份命令Windows环境下与Linux环境下的区别。报错： Couldn't find table: ">"
###发表时间：2014-07-16
###分类：mysql,Linux
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2092831" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2092831</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>在对mysql进行备份的时候，在Windows的环境下执行下面的命令</p> 
 <pre name="code" class="sql">D:/develop/develop_tools/mysql-5.6.15-winx64/bin/mysqldump.exe -hlocalhost -uroot -p123 pure_web &gt; D:/test/backup/pure_web.2014_07_16_16_37_56.sql</pre> 
 <p>报错：<span style="color: #ffff00; background-color: #ff0000;">Couldn't find table: "&gt;"</span></p> 
 <p>原因：Windows环境下，在cmd的dos界面，是可以执行的。但是在java的</p> 
 <pre name="code" class="java"> Process process = Runtime.getRuntime().exec(cmd);</pre> 
 <p>&nbsp;就会报错，因为java认不出定位符” &gt; " ，以为它是mysql导出的table，所以报错。</p> 
 <p>&nbsp;</p> 
 <p>解决：</p> 
 <p>&nbsp; &nbsp; 在Windows的环境下，需要将" &gt; " 进行修改，如下：</p> 
 <pre name="code" class="sql">D:/develop/develop_tools/mysql-5.6.15-winx64/bin/mysqldump.exe -hlocalhost -uroot -p123 pure_web -rD:/test/backup/pure_web.2014_07_16_16_37_56.sql</pre> 
 <p>&nbsp;这样就OK了。</p> 
 <p>当然在Linux的环境下，" &gt; " 是可以使用的。因为操作系统的不同，对” &gt; " 的含义就不同。</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;======================= 下面是 mysqldump 的文档 ===========================</p> 
 <div class="quote_title">
  mysqldump 写道
 </div> 
 <div class="quote_div">
  mysqldump Ver 10.13 Distrib 5.6.15, for Win64 (x86_64)
  <br>Copyright (c) 2000, 2013, Oracle and/or its affiliates. All rights reserved.
  <br>
  <br>Oracle is a registered trademark of Oracle Corporation and/or its
  <br>affiliates. Other names may be trademarks of their respective
  <br>owners.
  <br>
  <br>Dumping structure and contents of MySQL databases and tables.
  <br>Usage: mysqldump [OPTIONS] database [tables]
  <br>OR mysqldump [OPTIONS] --databases [OPTIONS] DB1 [DB2 DB3...]
  <br>OR mysqldump [OPTIONS] --all-databases [OPTIONS]
  <br>
  <br>Default options are read from the following files in the given order:
  <br>C:\windows\my.ini C:\windows\my.cnf C:\my.ini C:\my.cnf D:\baidu\develop\develop_tools\mysql-5.6.15-winx64\my.ini D:\baidu\develop\develop_tools\mysql-5.6.15-winx64\my.cnf 
  <br>The following groups are read: mysqldump client
  <br>The following options may be given as the first argument:
  <br>--print-defaults Print the program argument list and exit.
  <br>--no-defaults Don't read default options from any option file,
  <br> except for login file.
  <br>--defaults-file=# Only read default options from the given file #.
  <br>--defaults-extra-file=# Read this file after the global files are read.
  <br>--defaults-group-suffix=#
  <br> Also read groups with concat(group, suffix)
  <br>--login-path=# Read this path from the login file.
  <br> -A, --all-databases Dump all the databases. This will be same as --databases
  <br> with all databases selected.
  <br> -Y, --all-tablespaces 
  <br> Dump all the tablespaces.
  <br> -y, --no-tablespaces 
  <br> Do not dump any tablespace information.
  <br> --add-drop-database Add a DROP DATABASE before each create.
  <br> --add-drop-table Add a DROP TABLE before each create.
  <br> (Defaults to on; use --skip-add-drop-table to disable.)
  <br> --add-drop-trigger Add a DROP TRIGGER before each create.
  <br> --add-locks Add locks around INSERT statements.
  <br> (Defaults to on; use --skip-add-locks to disable.)
  <br> --allow-keywords Allow creation of column names that are keywords.
  <br> --apply-slave-statements 
  <br> Adds 'STOP SLAVE' prior to 'CHANGE MASTER' and 'START
  <br> SLAVE' to bottom of dump.
  <br> --bind-address=name IP address to bind to.
  <br> --character-sets-dir=name 
  <br> Directory for character set files.
  <br> -i, --comments Write additional information.
  <br> (Defaults to on; use --skip-comments to disable.)
  <br> --compatible=name Change the dump to be compatible with a given mode. By
  <br> default tables are dumped in a format optimized for
  <br> MySQL. Legal modes are: ansi, mysql323, mysql40,
  <br> postgresql, oracle, mssql, db2, maxdb, no_key_options,
  <br> no_table_options, no_field_options. One can use several
  <br> modes separated by commas. Note: Requires MySQL server
  <br> version 4.1.0 or higher. This option is ignored with
  <br> earlier server versions.
  <br> --compact Give less verbose output (useful for debugging). Disables
  <br> structure comments and header/footer constructs. Enables
  <br> options --skip-add-drop-table --skip-add-locks
  <br> --skip-comments --skip-disable-keys --skip-set-charset.
  <br> -c, --complete-insert 
  <br> Use complete insert statements.
  <br> -C, --compress Use compression in server/client protocol.
  <br> -a, --create-options 
  <br> Include all MySQL specific create options.
  <br> (Defaults to on; use --skip-create-options to disable.)
  <br> -B, --databases Dump several databases. Note the difference in usage; in
  <br> this case no tables are given. All name arguments are
  <br> regarded as database names. 'USE db_name;' will be
  <br> included in the output.
  <br> -#, --debug[=#] This is a non-debug version. Catch this and exit.
  <br> --debug-check Check memory and open file usage at exit.
  <br> --debug-info Print some debug info at exit.
  <br> --default-character-set=name 
  <br> Set the default character set.
  <br> --delayed-insert Insert rows with INSERT DELAYED.
  <br> --delete-master-logs 
  <br> Delete logs on master after backup. This automatically
  <br> enables --master-data.
  <br> -K, --disable-keys '/*!40000 ALTER TABLE tb_name DISABLE KEYS */; and
  <br> '/*!40000 ALTER TABLE tb_name ENABLE KEYS */; will be put
  <br> in the output.
  <br> (Defaults to on; use --skip-disable-keys to disable.)
  <br> --dump-slave[=#] This causes the binary log position and filename of the
  <br> master to be appended to the dumped data output. Setting
  <br> the value to 1, will printit as a CHANGE MASTER command
  <br> in the dumped data output; if equal to 2, that command
  <br> will be prefixed with a comment symbol. This option will
  <br> turn --lock-all-tables on, unless --single-transaction is
  <br> specified too (in which case a global read lock is only
  <br> taken a short time at the beginning of the dump - don't
  <br> forget to read about --single-transaction below). In all
  <br> cases any action on logs will happen at the exact moment
  <br> of the dump.Option automatically turns --lock-tables off.
  <br> -E, --events Dump events.
  <br> -e, --extended-insert 
  <br> Use multiple-row INSERT syntax that include several
  <br> VALUES lists.
  <br> (Defaults to on; use --skip-extended-insert to disable.)
  <br> --fields-terminated-by=name 
  <br> Fields in the output file are terminated by the given
  <br> string.
  <br> --fields-enclosed-by=name 
  <br> Fields in the output file are enclosed by the given
  <br> character.
  <br> --fields-optionally-enclosed-by=name 
  <br> Fields in the output file are optionally enclosed by the
  <br> given character.
  <br> --fields-escaped-by=name 
  <br> Fields in the output file are escaped by the given
  <br> character.
  <br> -F, --flush-logs Flush logs file in server before starting dump. Note that
  <br> if you dump many databases at once (using the option
  <br> --databases= or --all-databases), the logs will be
  <br> flushed for each database dumped. The exception is when
  <br> using --lock-all-tables or --master-data: in this case
  <br> the logs will be flushed only once, corresponding to the
  <br> moment all tables are locked. So if you want your dump
  <br> and the log flush to happen at the same exact moment you
  <br> should use --lock-all-tables or --master-data with
  <br> --flush-logs.
  <br> --flush-privileges Emit a FLUSH PRIVILEGES statement after dumping the mysql
  <br> database. This option should be used any time the dump
  <br> contains the mysql database and any other database that
  <br> depends on the data in the mysql database for proper
  <br> restore. 
  <br> -f, --force Continue even if we get an SQL error.
  <br> -?, --help Display this help message and exit.
  <br> --hex-blob Dump binary strings (BINARY, VARBINARY, BLOB) in
  <br> hexadecimal format.
  <br> -h, --host=name Connect to host.
  <br> --ignore-table=name Do not dump the specified table. To specify more than one
  <br> table to ignore, use the directive multiple times, once
  <br> for each table. Each table must be specified with both
  <br> database and table names, e.g.,
  <br> --ignore-table=database.table.
  <br> --include-master-host-port 
  <br> Adds 'MASTER_HOST=&lt;host&gt;, MASTER_PORT=&lt;port&gt;' to 'CHANGE
  <br> MASTER TO..' in dump produced with --dump-slave.
  <br> --insert-ignore Insert rows with INSERT IGNORE.
  <br> --lines-terminated-by=name 
  <br> Lines in the output file are terminated by the given
  <br> string.
  <br> -x, --lock-all-tables 
  <br> Locks all tables across all databases. This is achieved
  <br> by taking a global read lock for the duration of the
  <br> whole dump. Automatically turns --single-transaction and
  <br> --lock-tables off.
  <br> -l, --lock-tables Lock all tables for read.
  <br> (Defaults to on; use --skip-lock-tables to disable.)
  <br> --log-error=name Append warnings and errors to given file.
  <br> --master-data[=#] This causes the binary log position and filename to be
  <br> appended to the output. If equal to 1, will print it as a
  <br> CHANGE MASTER command; if equal to 2, that command will
  <br> be prefixed with a comment symbol. This option will turn
  <br> --lock-all-tables on, unless --single-transaction is
  <br> specified too (in which case a global read lock is only
  <br> taken a short time at the beginning of the dump; don't
  <br> forget to read about --single-transaction below). In all
  <br> cases, any action on logs will happen at the exact moment
  <br> of the dump. Option automatically turns --lock-tables
  <br> off.
  <br> --max-allowed-packet=# 
  <br> The maximum packet length to send to or receive from
  <br> server.
  <br> --net-buffer-length=# 
  <br> The buffer size for TCP/IP and socket communication.
  <br> --no-autocommit Wrap tables with autocommit/commit statements.
  <br> -n, --no-create-db Suppress the CREATE DATABASE ... IF EXISTS statement that
  <br> normally is output for each dumped database if
  <br> --all-databases or --databases is given.
  <br> -t, --no-create-info 
  <br> Don't write table creation info.
  <br> -d, --no-data No row information.
  <br> -N, --no-set-names Same as --skip-set-charset.
  <br> --opt Same as --add-drop-table, --add-locks, --create-options,
  <br> --quick, --extended-insert, --lock-tables, --set-charset,
  <br> and --disable-keys. Enabled by default, disable with
  <br> --skip-opt.
  <br> --order-by-primary Sorts each table's rows by primary key, or first unique
  <br> key, if such a key exists. Useful when dumping a MyISAM
  <br> table to be loaded into an InnoDB table, but will make
  <br> the dump itself take considerably longer.
  <br> -p, --password[=name] 
  <br> Password to use when connecting to server. If password is
  <br> not given it's solicited on the tty.
  <br> -W, --pipe Use named pipes to connect to server.
  <br> -P, --port=# Port number to use for connection.
  <br> --protocol=name The protocol to use for connection (tcp, socket, pipe,
  <br> memory).
  <br> -q, --quick Don't buffer query, dump directly to stdout.
  <br> (Defaults to on; use --skip-quick to disable.)
  <br> -Q, --quote-names Quote table and column names with backticks (`).
  <br> (Defaults to on; use --skip-quote-names to disable.)
  <br> --replace Use REPLACE INTO instead of INSERT INTO.
  <br>
  <span style="color: #ffff00; background-color: #ff9900;">-r, --result-file=name </span>
  <br> Direct output to a given file. This option should be used
  <br> in systems (e.g., DOS, Windows) that use carriage-return
  <br> linefeed pairs (\r\n) to separate text lines. This option
  <br> ensures that only a single newline is used.
  <br> -R, --routines Dump stored routines (functions and procedures).
  <br> --set-charset Add 'SET NAMES default_character_set' to the output.
  <br> (Defaults to on; use --skip-set-charset to disable.)
  <br> --set-gtid-purged[=name] 
  <br> Add 'SET @@GLOBAL.GTID_PURGED' to the output. Possible
  <br> values for this option are ON, OFF and AUTO. If ON is
  <br> used and GTIDs are not enabled on the server, an error is
  <br> generated. If OFF is used, this option does nothing. If
  <br> AUTO is used and GTIDs are enabled on the server, 'SET
  <br> @@GLOBAL.GTID_PURGED' is added to the output. If GTIDs
  <br> are disabled, AUTO does nothing. Default is AUTO.
  <br> --shared-memory-base-name=name 
  <br> Base name of shared memory.
  <br> --single-transaction 
  <br> Creates a consistent snapshot by dumping all tables in a
  <br> single transaction. Works ONLY for tables stored in
  <br> storage engines which support multiversioning (currently
  <br> only InnoDB does); the dump is NOT guaranteed to be
  <br> consistent for other storage engines. While a
  <br> --single-transaction dump is in process, to ensure a
  <br> valid dump file (correct table contents and binary log
  <br> position), no other connection should use the following
  <br> statements: ALTER TABLE, DROP TABLE, RENAME TABLE,
  <br> TRUNCATE TABLE, as consistent snapshot is not isolated
  <br> from them. Option automatically turns off --lock-tables.
  <br> --dump-date Put a dump date to the end of the output.
  <br> (Defaults to on; use --skip-dump-date to disable.)
  <br> --skip-opt Disable --opt. Disables --add-drop-table, --add-locks,
  <br> --create-options, --quick, --extended-insert,
  <br> --lock-tables, --set-charset, and --disable-keys.
  <br> -S, --socket=name The socket file to use for connection.
  <br> --ssl Enable SSL for connection (automatically enabled with
  <br> other flags).
  <br> --ssl-ca=name CA file in PEM format (check OpenSSL docs, implies
  <br> --ssl).
  <br> --ssl-capath=name CA directory (check OpenSSL docs, implies --ssl).
  <br> --ssl-cert=name X509 cert in PEM format (implies --ssl).
  <br> --ssl-cipher=name SSL cipher to use (implies --ssl).
  <br> --ssl-key=name X509 key in PEM format (implies --ssl).
  <br> --ssl-crl=name Certificate revocation list (implies --ssl).
  <br> --ssl-crlpath=name Certificate revocation list path (implies --ssl).
  <br> --ssl-verify-server-cert 
  <br> Verify server's "Common Name" in its cert against
  <br> hostname used when connecting. This option is disabled by
  <br> default.
  <br> -T, --tab=name Create tab-separated textfile for each table to given
  <br> path. (Create .sql and .txt files.) NOTE: This only works
  <br> if mysqldump is run on the same machine as the mysqld
  <br> server.
  <br> --tables Overrides option --databases (-B).
  <br> --triggers Dump triggers for each dumped table.
  <br> (Defaults to on; use --skip-triggers to disable.)
  <br> --tz-utc SET TIME_ZONE='+00:00' at top of dump to allow dumping of
  <br> TIMESTAMP data when a server has data in different time
  <br> zones or data is being moved between servers with
  <br> different time zones.
  <br> (Defaults to on; use --skip-tz-utc to disable.)
  <br> -u, --user=name User for login if not current user.
  <br> -v, --verbose Print info about the various stages.
  <br> -V, --version Output version information and exit.
  <br> -w, --where=name Dump only selected records. Quotes are mandatory.
  <br> -X, --xml Dump a database as well formed XML.
  <br> --plugin-dir=name Directory for client-side plugins.
  <br> --default-auth=name Default authentication client-side plugin to use.
  <br>
  <br>Variables (--variable-name=value)
  <br>and boolean options {FALSE|TRUE} Value (after reading options)
  <br>--------------------------------- ----------------------------------------
  <br>all-databases FALSE
  <br>all-tablespaces FALSE
  <br>no-tablespaces FALSE
  <br>add-drop-database FALSE
  <br>add-drop-table TRUE
  <br>add-drop-trigger FALSE
  <br>add-locks TRUE
  <br>allow-keywords FALSE
  <br>apply-slave-statements FALSE
  <br>bind-address (No default value)
  <br>character-sets-dir (No default value)
  <br>comments TRUE
  <br>compatible (No default value)
  <br>compact FALSE
  <br>complete-insert FALSE
  <br>compress FALSE
  <br>create-options TRUE
  <br>databases FALSE
  <br>debug-check FALSE
  <br>debug-info FALSE
  <br>default-character-set utf8
  <br>delayed-insert FALSE
  <br>delete-master-logs FALSE
  <br>disable-keys TRUE
  <br>dump-slave 0
  <br>events FALSE
  <br>extended-insert TRUE
  <br>fields-terminated-by (No default value)
  <br>fields-enclosed-by (No default value)
  <br>fields-optionally-enclosed-by (No default value)
  <br>fields-escaped-by (No default value)
  <br>flush-logs FALSE
  <br>flush-privileges FALSE
  <br>force FALSE
  <br>hex-blob FALSE
  <br>host (No default value)
  <br>include-master-host-port FALSE
  <br>insert-ignore FALSE
  <br>lines-terminated-by (No default value)
  <br>lock-all-tables FALSE
  <br>lock-tables TRUE
  <br>log-error (No default value)
  <br>master-data 0
  <br>max-allowed-packet 25165824
  <br>net-buffer-length 1046528
  <br>no-autocommit FALSE
  <br>no-create-db FALSE
  <br>no-create-info FALSE
  <br>no-data FALSE
  <br>order-by-primary FALSE
  <br>port 0
  <br>quick TRUE
  <br>quote-names TRUE
  <br>replace FALSE
  <br>routines FALSE
  <br>set-charset TRUE
  <br>shared-memory-base-name (No default value)
  <br>single-transaction FALSE
  <br>dump-date TRUE
  <br>socket (No default value)
  <br>ssl FALSE
  <br>ssl-ca (No default value)
  <br>ssl-capath (No default value)
  <br>ssl-cert (No default value)
  <br>ssl-cipher (No default value)
  <br>ssl-key (No default value)
  <br>ssl-crl (No default value)
  <br>ssl-crlpath (No default value)
  <br>ssl-verify-server-cert FALSE
  <br>tab (No default value)
  <br>triggers TRUE
  <br>tz-utc TRUE
  <br>user (No default value)
  <br>verbose FALSE
  <br>where (No default value)
  <br>plugin-dir (No default value)
  <br>default-auth (No default value)
 </div> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>