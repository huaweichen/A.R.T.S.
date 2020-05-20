# Install Ruby

[Install Ruby](https://jekyllrb.com/docs/installation/)
```bash
sudo apt-get install ruby-full build-essential zlib1g-dev

echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

# Install Jekyll

[Install Ruby](https://jekyllrb.com/docs/installation/)
```bash
gem install jekyll bundler

jekyll new myblog
cd myblog

bundle exec jekyll serve
# http://localhost:4000
```