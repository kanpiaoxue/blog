#git 关联编辑器软件（sublime）
###发表时间：2017-07-27
###分类：git,非技术
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2387114" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2387114</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>参考资料：&nbsp;</p> 
 <p><a href="https://help.github.com/articles/associating-text-editors-with-git/">https://help.github.com/articles/associating-text-editors-with-git/</a></p> 
 <p><a href="https://stackoverflow.com/questions/8951275/how-can-i-make-sublime-text-the-default-editor-for-git">https://stackoverflow.com/questions/8951275/how-can-i-make-sublime-text-the-default-editor-for-git</a></p> 
 <p>======================================================</p> 
 <div class="quote_title">
  写道
 </div> 
 <div class="quote_div">
  Using Atom as your editor
  <br>You can set your default editor in Git to use Atom if you have installed the editor.
  <br>1、Install Atom.
  <br> Open Terminal.
  <br> Type this command:
  <br> $ git config --global core.editor "atom --wait"
  <br>2、Using Sublime Text as your editor
  <br> You can set your default editor in Git to use Sublime Text 3.
  <br> Install Sublime Text 3.
  <br> Open Terminal.
  <br> Type this command:
  <br> $ git config --global core.editor "subl -n -w"
  <br>3、Using TextMate as your editor
  <br> You can set your default editor in Git to use Textmate if you have installed the mate command.
  <br> Install mate
  <br> Open Terminal.
  <br> Type this command:
  <br> $ git config --global core.editor "mate -w"
 </div> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>======================================================</p> 
 <p>我设置 sublime text3 为自己的 git 提交编辑器。如下：</p> 
 <p>Mac 的设置 写道</p> 
 <p>git config --global core.editor "'/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl' -n -w"</p> 
 <p>&nbsp;这里的 sublime text3 的目录需要自己来根据情况来修改。其实就是找到sublime text3的安装目录，找到它的运行程序，将这个完整的运行程序的目录写在这里。</p> 
 <p>&nbsp;</p> 
</div>