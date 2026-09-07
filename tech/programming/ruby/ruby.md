# Ruby

### Github-Pages/Jekyll

- Jekyll is a Ruby-based static site generator that generates HTML from Markdown.
- GitHub pages is a static site generator built on top of Jeckyll.
- It is used for github.io sites e.g. https://bretttolbert.github.io/
- However on my privately hosted site https://bretttolbert.com,
instead of using GitHub pages, I use Jekyll with the github-pages theme.
- This makes the appearance of bretttolbert.com consistent with brettolbert.github.io.

### Install ruby-build

- Do not install the default Ubuntu version of `ruby-build` using `apt`, it is very outdated
- If it is installed, remove it with `sudo apt remove ruby-build`
- Install the self-updating Git version:
```bash
git clone https://github.com/rbenv/ruby-build.git "$(rbenv root)"/plugins/ruby-build
```

### Update ruby-build

```bash
git -C "$(rbenv root)"/plugins/ruby-build pull
```

### Add ruby-build to PATH

```bash
export PATH="$(rbenv root)"/plugins/ruby-build/bin:$PATH
# e.e.:
export PATH=/home/brett/.rbenv/plugins/ruby-build/bin:$PATH
```

### List available versions

```bash
ruby-build --definitions | grep -E '^3\.[234]\.[0-9]+$'
```

### Install latest version

```bash
rbenv install 3.4.10
```

### Switch to specified version

```bash
rbenv local 3.4.10
```

### Fix missing shell initialization

If rbenv global is not switching your system's Ruby version, it is almost always caused by missing shell initialization configs or local directory overrides. To fix this, check the most common culprits:

1. Missing Shell Initialization (Most Common)

If you never ran rbenv init, your command line does not know where to look for your rbenv versions. You must add the initialization script to your shell profile.

For Bash shell, enter the corresponding commands below:

```bash
echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
source ~/.bash_profile
```

### View currently active version

```bash
rbenv version
```

### Install completely isolated openssl 1.1

Modern Linux distributions (e.g. Ubuntu 24.04 and later) completely dropped OpenSSL 1.1 from their default package trees.

To install a completely isolated instance of OpenSSL 1.1 on Ubuntu (avoiding conflicts with your system's OpenSSL 3.x), you can compile it from source and install it in a custom directory (e.g., /opt/openssl-1.1).

```bash
sudo apt update
sudo apt install -y build-essential zlib1g-dev

cd /tmp
wget https://github.com/openssl/openssl/releases/download/OpenSSL_1_1_1w/openssl-1.1.1w.tar.gz
tar -xvzf openssl-1.1.1w.tar.gz
cd openssl-1.1.1w

./config --prefix=/opt/openssl-1.1 --openssldir=/opt/openssl-1.1 shared zlib
make
make test
sudo make install

```

### Install deps for Jekyll (Ruby 2.7)

Github-Pages uses Jekyll 3.9, which isn’t compatible with Ruby 3. Downgrading to Ruby 2.7 should avoid the problem.

However Ruby 2.7 requires OpenSSL 1.1 (see above for installation).

```bash
RUBY_CONFIGURE_OPTS="--with-openssl-dir=/opt/openssl-1.1" rbenv install 2.7.6
rbenv global 2.7.6
gem install unf
gem install rake
gem install bundler:2.3.7
rm -rf vendor/
bundle install
```

Note: `vendor/` is basically the Ruby equivalent of the `node_modules/` folder. It can be safely deleted.


```bash
sudo apt install ruby-full build-essential zlib1g-dev
```
