# go

Disable GO111 module (something I tried to work around an error, probably not the best solution)
```bash
go env -w GO111MODULE=off
```

## Misc commands that didn't work:

```bash
go install github.com/dhowden/tag/cmd/tag@latest
```

```bash
go get -d github.com/dhowden/tag/cmd/tag@latest
```

```
$ git clone https://github.com/dhowden/tag $GOPATH/src/github.com/dhowden/tag
```
