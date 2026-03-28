# 关于Git Bash提交时的问题解决记录  
***
#### 1. 在我按照网上用Git Bash推送文档到远程仓库的方法后，我发现Git Bash进行了报错：**getaddrinfo() thread failed to start**  
   * AI对此进行了分析认为是我的**网络连接问题**，但是我使用的是自己手机开的流量热点，我感觉是网络问题的可能性比较低，我对AI进行了二次询问。  
#### 2. AI这次认为有可能是**DNS解析失败**（手机网络DNS无法解析GitHub），且继续认为是网络方面的问题，提供了两种方法  
   * **方法一（重试+修复DNS）**：先清理Git的网络配置（避免之前的错误配置影响）给了我下面的代码给我复制粘贴  
```  
git config --global --unset http.proxy
git config --global --unset https.proxy
git config --global http.sslVerify false  
```  
  粘贴完后再进行推送：git push -u origin master 可是经过尝试之后还是失败了。  
  * **方法二（换用SSH方式推送，可以绕开网络限制）：**  
![](2026-03-27-16-00-25.png)  
这个方法**成功生成了SSH密钥**。  
#### 3. 在得到了在SSH中的公钥和私钥后，进行了以下步骤  
   * 打开并复制公钥内容  
   * 登录GitHub，添加SSH密钥  
   * 移除旧的HTTPS关联，再关联SSH地址  
   * 最后推送到GitHub中：git push -u origin master  
      
  ***经过以上尝试后成功完成了Git Bash推送文档到远程仓库的任务***  
***  
## 在GitHub的Tasks-仓库中创建了两个分支,要取得合并  
1. 要合并的**原因复盘**：在第一阶段的时候我是通过**网页端**提交的任务，提交到了GitHub中Tasks-仓库的**main**中。在第二阶段的时候，是通过**Git Bash**提交的，但由于操作不当，在初始操作的时候新建了一个master分支，并且后续的所有文档都被默认提交到了master分支中，但我想要把所有的文档都放到同一个分支中，这样更利于复习与任务考核  
2. 为此我进行了以下操作：  
    1. **先拉取最新代码（避免冲突）**：在本地的test文件夹中打开bash输入：  
     git checkout master   
    git pull origin master  
    2. **创建并切换到main分支**:  
    git checkout -b main  
    3. **推送main分支到远程，并绑定为默认推送分支**：  
   git push -u origin main


