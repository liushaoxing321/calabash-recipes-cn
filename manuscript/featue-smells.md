# Feature 臭味
虽然 Feature 部分描述的是用户的需求，但也是代码，所以出现臭味也需要重构。

## 不要包含与业务无关的数据. 
比如以下场景中包含用户名和密码，一定不是业务的要求，而后面的提示消息或许就是业务的要求了。

    当我使用用户名"tom"和密码"s3cr3t"登录时会提示"用户名与密码不匹配"

## 不要有具体的场景操作.
比如以下场景有具体的场景操作，如果发生一些界面调整，那就不得不修改验收测试了，而且维护成本偏高

    当我在"用户名"中输入"tom"
    同时我在"密码"中输入"s3cr3t"
    并且我点击"登录"

## 场景测试不要文不对题.
比如以下是确认添加好友验证的场景，却包含了发送消息到验收测试

    场景：确认好友请求
      当我确认好友的请求后
      那么我可以立刻给好友发送消息

## 一个场景不要包含多个验收条件.
比如以下场景要拆分成多个

    场景：给好友发送消息
      当我和好友聊天的时候
      那么我可以给好友发送文本消息
      并且我可以给好友发送图片消息
      并且我可以给好友发送位置消息

## 要使用业务语言来描述验收场景, 不要使用技术语言.
比如"服务器"是个什么东西? 客户不知道也不需要知道.

    场景：登录失败
       假如我使用无效的用户名和密码登录
       那么服务器会给我返回登录失败的消息

## 验收测试中不要包含边界测试.
比如以下场景的测试案例应该由单元测试来覆盖

    场景：空用户名
      假如我使用用户名""注册账号
      那么我可以看到无效用户名的错误消息

    场景：空白用户名
      假如我使用用户名"     "注册账号
      那么我可以看到无效用户名的错误消息
     
    场景: 用户名中包含非法字符
      假如我使用用户名"abc@#$%^&*()"注册账号
      那么我可以看到无效用户名的错误消息

## 验收测试要能够独立执行, 不要互相依赖.
比如：以下场景在执行一次之后，是否能够重复执行

    场景: 添加好友
      假如我已经有好友
      那么我可以删除好友

## 一个功能的所有场景如果需要相同的假设，就放到“背景”中
比如：以下场景的假设需要放到背景中

    场景：给好友发送文本消息
      假如我已经登录
      # ...
     
    场景：给好友发送图片消息
      假如我已经登录
      # ...
     
    场景：给好友发送位置消息
      假如我已经登录
      # ...