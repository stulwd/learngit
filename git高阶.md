# git合并逻辑

### fork:

​	复制一份别人的repo到自己的仓库，不会和源repo保持同步

---

### pull request:

发起一个请求，请求源repo作者合并自己的代码。
详细介绍：当自己对fork来的仓库做了修改并commit后，可以创建一个pull request给源repo让其merge，在发起PR的时候，会有“是否允许自己的代码被修改”选项，若勾选，则当合并发生冲突，允许源仓库作者解决冲突，并将解决后的commit自动同步到自己的repo，若不勾选，则发生冲突时，对方解决不了冲突，只能我们自己解决，然后再次pull request。

- PR时冲突的两个必要条件：
  - 对方的commit比自己前一次的commit要新
  - 冲突来源于在同一个文件上的修改  

若只是不同文件上的冲突，即使对方commit比自己新，也不会发生冲突，可以正常合并，若是同一文件上的冲突，例如自己修改某一行代码，产生新的commit，实际上在git里这并不叫冲突，可以正常合并。
这也证明了git先监测的是commit，若commit不冲突，一定不冲突，若commit冲突，没有同一文件冲突，则一定不冲突，有同一文件冲突，则是冲突，需解决。
pull request可以选择从从哪个repo合并到哪个repo，包括本仓的两个不同分支合并，不一定要pr到源repo，所以pull request也可以从源repo到自己的repo，然后自己接受pr，从而实现同步的目的。

---

### contributor：

- 给项目添加合作者：

  在项目主页的setting->Manage access->invite a collaborator,邀请一个协同开发者contributor，对方接受邀请后，就有了写此仓库权限，包括push。
  添加完权限后，在其他计算机上试验一下，clone这个项目后，做一些修改并提交，然后git push，会让你输入github账号密码，然后就能成功push。

- 限制某一分支的push权限给部分开发者：
  只限企业版和付费版用户。在项目setting->branches里设置。

---

### 关于push：

你只能比远程新，否则，需要先pull，再push。
所以当远程比你的commit新，即使远程和你的修改不是同一文件（在PR时或者merge时不会发生冲突），也需要你先PULL，再push。