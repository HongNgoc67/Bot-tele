version: 2
jobs:
  build:
    docker:
      - image: circleci/golang:1.13
    working_directory: /go/src/github.com/go-chat-bot/bot
    steps:
      - checkout
      - run: go test -v -cover -race -coverprofile=coverage.out          
      - run: go get github.com/mattn/goveralls
      - run: goveralls -coverprofile=coverage.out -service=circle-ci -repotoken=$COVERALLS_TOKEN
