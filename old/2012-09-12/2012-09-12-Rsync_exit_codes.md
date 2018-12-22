#Rsync exit codes
###发表时间：2012-09-12
###分类：rsync
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1676827" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1676827</a>

---

<p> </p>
<p style="margin-top: 0.4em; margin-bottom: 0.5em; line-height: 19.200000762939453px; font-family: sans-serif; font-size: 13px;">This is a list of rsync exit codes (rsync status codes / rsync error codes).</p>
<pre>       0      Success
       1      Syntax or usage error
       2      Protocol incompatibility
       3      Errors selecting input/output files, dirs
       4      Requested  action not supported: an attempt was made to manipulate 64-bit files on a platform 
              that cannot support them; or an option was specified that is supported by the client and not by the server.
       5      Error starting client-server protocol
       6      Daemon unable to append to log-file
       10     Error in socket I/O
       11     Error in file I/O
       12     Error in rsync protocol data stream
       13     Errors with program diagnostics
       14     Error in IPC code
       20     Received SIGUSR1 or SIGINT
       21     Some error returned by waitpid()
       22     Error allocating core memory buffers
       23     Partial transfer due to error
       24     Partial transfer due to vanished source files
       25     The --max-delete limit stopped deletions
       30     Timeout in data send/receive
       35     Timeout waiting for daemon connection
</pre>
<p style="margin-top: 0.4em; margin-bottom: 0.5em; line-height: 19.200000762939453px; font-family: sans-serif; font-size: 13px;"><br>Error code 11 can be confusing when rsync is started as a service on a Windows platform. It can mean that the pid file for rsync already exists in the C:\Program Files\cwRsyncServer folder (or ony other directory where rsync is installed) - although no other info will be given in Windows Event Log. It will become more apparent only if rsync is started as a service from the command line.</p>
<p style="margin-top: 0.4em; margin-bottom: 0.5em; line-height: 19.200000762939453px; font-family: sans-serif; font-size: 13px;">&nbsp;</p>
<p style="margin-top: 0.4em; margin-bottom: 0.5em; line-height: 19.200000762939453px; font-family: sans-serif; font-size: 13px;">原文：&nbsp;<a href="http://wpkg.org/Rsync_exit_codes">http://wpkg.org/Rsync_exit_codes</a></p>