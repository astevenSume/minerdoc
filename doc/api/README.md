开始使用
------------------------------

### 需要

 - **Linux 或者 macOS** — Windows 可能可以，但不是被支持的.
 - **Ruby, 版本 2.3.1 以上**
 - **Bundler**

#### 推荐使用 rbenv 来管理 ruby

参考 [ruby 的 osx 安装文档](https://gorails.com/setup/osx/10.14-mojave)
```shell
brew install rbenv ruby-build

# Add rbenv to bash so that it loads every time you open a terminal
echo 'if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi' >> ~/.bash_profile
source ~/.bash_profile

# Install Ruby
rbenv install 2.6.1
rbenv global 2.6.1
ruby -v
gem install bundler -v 1.7.3
```

#### 默认方式安装 ruby

```shell
brew update
brew install ruby
gem install bundler -v 1.7.3
```

这里注意 bundler 2.0.1 版本不兼容, 只能使用旧版本的 bundler.

### 安装

```shell
bundle install
bundle exec middleman server
```

你可以在 http://localhost:4567 查看你的文档.

### 使用
- [Markdown 语法](https://github.com/lord/slate/wiki/Markdown-Syntax)
- [发布文档](https://github.com/lord/slate/wiki/Deploying-Slate).
