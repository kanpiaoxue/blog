#ubuntu上面apt-get的小记
###发表时间：2017-08-23
###分类：Linux,ubuntu
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2390908" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2390908</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <div class="quote_title">
  apt-get常用 写道
 </div> 
 <div class="quote_div">
  apt-get update #更新本地索引
  <br>apt-cache search all #显示可以按照的软件
  <br>apt-get install xxx #安装软件
  <br>apt-get remove xxx #卸载软件
 </div> 
 <p>&nbsp;</p> 
 <div class="quote_title">
  apt-get的帮助内容 写道
 </div> 
 <div class="quote_div">
  root@4242342343:/# apt-get --help
  <br>apt 1.2.24 (amd64)
  <br>Usage: apt-get [options] command
  <br> apt-get [options] install|remove pkg1 [pkg2 ...]
  <br> apt-get [options] source pkg1 [pkg2 ...]
  <br>
  <br>apt-get is a command line interface for retrieval of packages
  <br>and information about them from authenticated sources and
  <br>for installation, upgrade and removal of packages together
  <br>with their dependencies.
  <br>
  <br>Most used commands:
  <br> update - Retrieve new lists of packages
  <br> upgrade - Perform an upgrade
  <br> install - Install new packages (pkg is libc6 not libc6.deb)
  <br> remove - Remove packages
  <br> purge - Remove packages and config files
  <br> autoremove - Remove automatically all unused packages
  <br> dist-upgrade - Distribution upgrade, see apt-get(8)
  <br> dselect-upgrade - Follow dselect selections
  <br> build-dep - Configure build-dependencies for source packages
  <br> clean - Erase downloaded archive files
  <br> autoclean - Erase old downloaded archive files
  <br> check - Verify that there are no broken dependencies
  <br> source - Download source archives
  <br> download - Download the binary package into the current directory
  <br> changelog - Download and display the changelog for the given package
  <br>
  <br>See apt-get(8) for more information about the available commands.
  <br>Configuration options and syntax is detailed in apt.conf(5).
  <br>Information about how to configure sources can be found in sources.list(5).
  <br>Package and version choices can be expressed via apt_preferences(5).
  <br>Security details are available in apt-secure(8).
  <br> This APT has Super Cow Powers.
 </div> 
 <p>&nbsp;</p> 
</div>