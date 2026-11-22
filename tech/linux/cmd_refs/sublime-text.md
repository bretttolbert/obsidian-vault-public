# sublime-text

## See also
- [alias](./alias.md)
- [curl](./curl.md)
- [vim](./vim.md)

## Install/update sublime-text
(replace `4121` with latest build number)
```bash
sudo rm -rf /opt/sublime-text && \
curl https://download.sublimetext.com/sublime_text_build_4121_x64.tar.xz -o st.tar.xz && \
sudo tar -xvf st.tar.xz -C /opt/ && \
rm st.tar.xz
```

## Set `subl` alias for sublime-text
```bash
alias subl='/opt/sublime_text/sublime_text'
```
## Meta: Sublime find/replace singlequote markdown code block with multiline bash markdown code block
- Find: ``([^`\r\n]+)``
- Replace: ````bash\n$1\n````

###### View graphical disc space usage using baobab
```bash
sudo baobab
```
