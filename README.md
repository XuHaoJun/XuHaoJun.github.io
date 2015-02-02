# [XuHaoJun’s blog](http://xuhaojun.github.io/)
Just put my static blog site into github page powered by [hugo](https://github.com/spf13/hugo).

## Build
``` sh
# Clone repo
git clone https://github.com/XuHaoJun/XuHaoJun.github.io.git blog

# Clone theme
cd blog
git checkout source
git submodule init
git submodule update

# Generate static site
hugo
```
