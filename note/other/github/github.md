
# ssh
## 生成ssh秘钥
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

ssh-keygen -t rsa -C "yi@edmodo.com"

## 验证
ssh -T git@github.com

## 参考
https://docs.github.com/cn/github/authenticating-to-github/testing-your-ssh-connection

