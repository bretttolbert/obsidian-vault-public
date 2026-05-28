# ruby

## Fix missing shell initialization

If rbenv global is not switching your system's Ruby version, it is almost always caused by missing shell initialization configs or local directory overrides. To fix this, check the most common culprits:

1. Missing Shell Initialization (Most Common)

If you never ran rbenv init, your command line does not know where to look for your rbenv versions. You must add the initialization script to your shell profile.

For Bash shell, enter the corresponding commands below:

```bash
echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
source ~/.bash_profile
```

## Install deps for Jekyll

```bash
rbenv install -v 3.1.2
rbenv global 3.1.2
gem install unf
gem install rake
rm -rf vendor/
bundle install
```

