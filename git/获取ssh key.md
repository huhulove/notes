1、打开Git Bash ，执行以下命令:
ssh-keygen -t rsa -C “your email”

2、默认Enter 执行

3、获取ssh key
cat ~/.ssh/id_rsa.pub

**修改git用户名何邮箱**

修改git用户名
git config --global user.name 你的目标用户名；

修改邮箱名
git config --global user.email 你的目标邮箱名;