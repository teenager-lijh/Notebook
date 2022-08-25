## 锁定的 main

问题：远程服务器拒绝!(Remote Rejected)

如果你是在一个大的合作团队中工作, 很可能是main被锁定了, 需要一些Pull Request流程来合并修改。如果你直接提交(commit)到本地main, 然后试图推送(push)修改, 你将会收到这样类似的信息:

! [远程服务器拒绝] main -> main (TF402455: 不允许推送(push)这个分支; 你必须使用pull request来更新这个分支.)

为什么会被拒绝？

远程服务器拒绝直接推送(push)提交到main, 因为策略配置要求 pull requests 来提交更新.

你应该按照流程,新建一个分支, 推送(push)这个分支并申请pull request,但是你忘记了并直接提交给了main.现在你卡住并且无法推送你的更新.



## 翻译一下：

搜索到的理解：这次也是常见的场景应用之一，之所以称之为锁定main，是因为在我们大公司开发中，我们不会这么顺利的就push自己想要的东西上去，不然人人都推自己觉得ok的不久乱套了嘛，所以管理者会为此设置为远程直接push 到main分支，会拒绝，策略配置要求 pull requests 来提交更新，pull request就理解成一种提醒一种请求，告诉管理者我要更新。
所以解决方案：新建一个分支feature, 推送到远程服务器. 因为远程不会允许直接push到main，所以我们可以推一个其他分支到远程，再请求pull request即可，合并的事情交给远程。这里还有一个问题，我们之后需要reset main分支和远程服务器保持一致, 否则下次你pull 的同时呢，他人的提交和你有冲突，这就会有问题啦。

我的理解：总的来说就是远程并不允许直接推送 main 分支的内容到远程仓库去，如果能够直接推送到 main 分支可能会乱套，所以相处了一种方法，使用 feature 分支来推送自己想要往 main 分支上推送的内容，然后由远程仓库的管理员来检查推送到远程仓库的 feature 分支上的内容是否正确，然后由管理员合并 feature 分支的数据到远程仓库的 main 分支上。要知道，创建 feature 分支其实就是让 feature 这个指针指向了当前 main 指向的节点，也就是说推送 feature 分支到远程的数据和我想要推送 main 分支到远程的数据是一样的。之所以在本地推送完成 feature 分支后还要 reset 我的 main 分支回去，这是为了保证我当前的本地 main 分支和远程的 main 分支以及远程仓库的 main 分支的状态一致，这样当我拉取远程仓库的数据的时候，就不会因为冲突而不能合并了，但是自己还想用刚写好的自己的代码，所以最后让本地 main 分支指向 o/main 分支指向的节点后，再让 HEAD 指向本地 feature 分支，以便继续工作。



## 搜索到的示例

1. 初始状态：当前本地分支 main 所指向的记录是我想推送到远程的记录，而我推送完成后应该让 main 指向 C1 这条记录

![image-20220630163726023](08-%E9%94%81%E5%AE%9A%E7%9A%84%20main.assets/image-20220630163726023-16565782470644.png)

2. `git checkout -b feature` 创建feature分支

![image-20220630163744805](08-%E9%94%81%E5%AE%9A%E7%9A%84%20main.assets/image-20220630163744805.png)

3. `git push origin feature` 提交feature这个分支到远程

![image-20220630163820904](08-%E9%94%81%E5%AE%9A%E7%9A%84%20main.assets/image-20220630163820904.png)

4. `git checkout main` 切换回 main 分支
   `git reset --hard o/main` 如果我们不reset回原来，这时候如果有人在远程提交更新了main分支，这时我们选择git pull，有一定的几率是我们在main修改的内容和别人修改的内容有冲突的地方，这时候git无法知道以谁的为准进行修改就merge失败了。

![image-20220630164034246](08-%E9%94%81%E5%AE%9A%E7%9A%84%20main.assets/image-20220630164034246.png)

5. 最后再让 HEAD 指向本地的 `feature` 分支

`git switch feature`

![image-20220701083747083](08-%E9%94%81%E5%AE%9A%E7%9A%84%20main.assets/image-20220701083747083.png)



## 解决方法

新建一个分支 feature, 推送到远程服务器. 然后reset你的main分支和远程服务器保持一致, 否则下次你pull并且他人的提交和你冲突的时候就会有问题.



## 游戏答案

见下边的实现过程



## 实现过程

1. 在游戏一开始的位置新建一个 `feature` 分支：

   `git checkout -b feature`

![image-20220701083033706](08-%E9%94%81%E5%AE%9A%E7%9A%84%20main.assets/image-20220701083033706.png)



2. 推送 `feature` 分支到远程仓库：

   `git push origin feature`

![image-20220701083238451](08-%E9%94%81%E5%AE%9A%E7%9A%84%20main.assets/image-20220701083238451.png)



3. 切换 HEAD 指向 main 分支
   `git switch main`

![image-20220701083352642](08-%E9%94%81%E5%AE%9A%E7%9A%84%20main.assets/image-20220701083352642.png)



4. 回退 main 分支到 o/main 的位置：

`git reset main o/main`

![image-20220630164034246](08-%E9%94%81%E5%AE%9A%E7%9A%84%20main.assets/image-20220630164034246.png)



5. 最后让 HEAD 指向 feature 分支：

`git switch feature`

![image-20220701084145676](08-%E9%94%81%E5%AE%9A%E7%9A%84%20main.assets/image-20220701084145676.png)
