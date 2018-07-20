# Dart Proof of concept

## Install
```
# Install dart
$ brew tap dart-lang/dart
# Get dev channel release:
$ brew install dart --devel
```

### CLI tools
```
$ pub global activate webdev
$ pub global activate stagehand
# then, add `export PATH=$PATH:~/.pub-cache/bin` into `.profile`
# in my case, `~/.bash_profile`
```

- `webdev`는 웹 앱을 빌드하고 서빙할 수 있도록 도와주는 CLI다.
`Dart`의 `build_runner`를 기반으로 만들어졌으며, `pub build`와 `pub
serve`를 대체한다.
- `stagehand`는 스캐폴딩 제너레이터이다.

## Syntax highlighting on vim
```
" .vimrc

" https://github.com/dart-lang/dart-vim-plugin
Plugin 'dart-lang/dart-vim-plugin'
```

## Create a web application
```
# create directory and move to the directory
$ mkdir dart-webapp
$ cd dart-webapp
# create project
$ stagehand web-simple
# install packages
$ pub get
```

## Run the application
```
$ webdev serve
```

- `webdev`로 첫 빌드 및 서빙에는 속도가 느리지만, 다음부터는 파일들이
캐싱되어 빨라질 것이다.
