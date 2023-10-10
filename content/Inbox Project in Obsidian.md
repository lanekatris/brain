The below steps don't exactly correlate to the current state of this project.

# How it works now
1. On desktop/mobile add a URL to the `Inbox` collection in [[Raindrop IO]]
2. When on desktop, run macro `syncInbox`
3. The URLs are now as files in the root of my Obsidian vault (the bookmarks are deleted in Raindrop.io as well)

# How it's implemented
- Using SaaS Raindrop.io chrome extension and mobile app
- n8n talks to Raindrop.io to get and delete bookmarks
- n8n has a webhook I call from Obsidian
- When the webhook is called the flow creates files then deletes the bookmark from the collection

> [!info]
> This is a pull based approach, not push. So this can either be scheduled or ran manually

# Stage 1 - Desktop Support
- [x] Create Js or Go code that takes a URL, creates a file in the root of the vault, and labels it and puts some content into the note. Somewhat similar to what I did in .NET for bookmarks ✅ 2023-07-11
- [x] Tweak the Chrome extension with an input and asubmit button in form that sends off to the api in the step above ^^^ ✅ 2023-07-11
- [x] Give an indicator that it was sent and its ok to kill the tab ✅ 2023-07-11
- [x] Fix the invalid file names ✅ 2023-07-16

# Stage 2 - Thinking about Bigger picture (cli, docker, lambda)
- [x] Wipe out old nx.dev folder ✅ 2023-07-18
- [x] Create new nx.dev and move scorecard parsing to ✅ 2023-07-18
- [x] Create easy script to copy transpiled code to obsidian dir, maybe golang should do this ✅ 2023-07-18
- [x] Fix my scripts to be in the correct format for macros ✅ 2023-07-18
- [x] Create macro to `Invoke: Refresh All Data` with the script above ^^^ ✅ 2023-07-18
- [x] Add parsing of scorecards to the above golang and macro script [[Disc Golf Course Map Overlay]] ✅ 2023-07-19
- [x] Create 2 executables, `lk` and `lkat` to be like docker and docker backend. [Reference](https://stackoverflow.com/questions/50904560/how-to-structure-go-application-to-produce-multiple-binaries) ✅ 2023-07-19

**Consumer**
- [x] Create obsidian macro repo in github ✅ 2023-07-19
- [x] Do files exist, if yes dl them into vault, then delete or move them else where on dir or bucket ✅ 2023-07-28
# Stretch
- [x] Grpc method ✅ 2023-07-28

# Ideas How To Implement
- [[Inbox Project in Obsidian#Stage 1 - Desktop Support]]
- raindrop - I'd have to clean this up though after I read an article. So its kind of like an external data maintenance. If I use obsidian ITS FILES that I just delete. Plus when I do the raindrop.io dump... I don't want people seeing the random stuff I want to read/revisit

# Thought Stream
* [localhost:8080/inbox/submit?url=https://www.mironov.com/owe/](http://localhost:8080/inbox/submit?url=https://www.mironov.com/owe/)
* [Go by Example: Writing Files](https://gobyexample.com/writing-files)
* [Go by Example: URL Parsing](https://gobyexample.com/url-parsing)
* [Format a time or date [complete guide] · YourBasic Go](https://yourbasic.org/golang/format-parse-string-time-date-example/)
* [Different ways to concatenate two strings in Golang - GeeksforGeeks](https://www.geeksforgeeks.org/different-ways-to-concatenate-two-strings-in-golang/)
* [Format a time or date [complete guide] · YourBasic Go](https://yourbasic.org/golang/format-parse-string-time-date-example/)
* [CSS · Bootstrap](https://getbootstrap.com/docs/3.4/css/#buttons)


# 2023-07-17  thought stream
* [NextJS: Simple Upload file to server - CodeSandbox](https://codesandbox.io/s/nextjs-simple-upload-file-to-server-thyb0?file=/pages/api/file.js)
* [reactjs - React Typescript: Get files from file input - Stack Overflow](https://stackoverflow.com/questions/59233036/react-typescript-get-files-from-file-input)
* [How to build a file uploader with Next.js and formidable](https://codersteps.com/articles/how-to-build-a-file-uploader-with-next-js-and-formidable)
* [node.js - How does one debug NextJS React apps with WebStorm? - Stack Overflow](https://stackoverflow.com/questions/54354389/how-does-one-debug-nextjs-react-apps-with-webstorm)
* [How to Implement an Uploading Service to S3 using NodeJS and TypeScript](https://messaismael.com/2022-03-29-how-to-Implement-an-uploading-service-to-s3-using-nodejs-and-typescript/)
* [amazon s3 - How can I Upload file to S3 using Next JS with Zeit Now and formidable-serverless - Stack Overflow](https://stackoverflow.com/questions/62845793/how-can-i-upload-file-to-s3-using-next-js-with-zeit-now-and-formidable-serverles)
* [Uploading Files using Formidable in a Node.js Application | Engineering Education (EngEd) Program | Section](https://www.section.io/engineering-education/uploading-files-using-formidable-nodejs/)


# 2023-07-19 Thought Stream
* [How to structure Go application to produce multiple binaries? - Stack Overflow](https://stackoverflow.com/questions/50904560/how-to-structure-go-application-to-produce-multiple-binaries)
* [avelino/awesome-go: A curated list of awesome Go frameworks, libraries and software](https://github.com/avelino/awesome-go#command-line)
* [charmbracelet/bubbletea: A powerful little TUI framework 🏗](https://github.com/charmbracelet/bubbletea)
* [golang cli framework - Google Search](https://www.google.com/search?q=golang+cli+framework&oq=golang+cli+framework&aqs=chrome..69i57j0i22i30j0i390i650.2812j0j7&sourceid=chrome&ie=UTF-8)
* [urfave/cli: A simple, fast, and fun package for building command line apps in Go](https://github.com/urfave/cli)
* [cobra/site/content/user\_guide.md at main · spf13/cobra](https://github.com/spf13/cobra/blob/main/site/content/user_guide.md)
* [Basics tutorial | Go | gRPC](https://grpc.io/docs/languages/go/basics/)
* [Golang gRPC Example - Earthly Blog](https://earthly.dev/blog/golang-grpc-example/)
* [Protocol Buffer Compiler Installation | gRPC](https://grpc.io/docs/protoc-installation/)
* [Go Generated Code Guide | Protocol Buffers Documentation](https://protobuf.dev/reference/go/go-generated/#package)
* [Go gRPC Beginners Tutorial | TutorialEdge.net](https://tutorialedge.net/golang/go-grpc-beginners-tutorial/)
* [Golang gRPC Tutorial: Building High-Performance Web Services](https://www.bacancytechnology.com/blog/golang-grpc#prerequisites-for-golang-grpc-example)
* [protocol buffers - protoc-gen-go-grpc: program not found or is not executable - Stack Overflow](https://stackoverflow.com/questions/60578892/protoc-gen-go-grpc-program-not-found-or-is-not-executable)
* [Support for required fields in proto3 via options · Issue #1468 · protobufjs/protobuf.js](https://github.com/protobufjs/protobuf.js/issues/1468)
* [go gin - Why can't I start two servers in the same Go project? - Stack Overflow](https://stackoverflow.com/questions/66955534/why-cant-i-start-two-servers-in-the-same-go-project)
* [NathanBaulch/protoc-gen-cobra: Cobra command line tool generator for gRPC clients](https://github.com/NathanBaulch/protoc-gen-cobra)
* [Using context.Context with cobra - Marcelo Bytes](https://blog.ksub.org/bytes/2019/10/07/using-context.context-with-cobra/)
* [Add support for context.Context by burdiyan · Pull Request #893 · spf13/cobra](https://github.com/spf13/cobra/pull/893)
* [cobra-context-demo command - github.com/mem/cobra-context-demo - Go Packages](https://pkg.go.dev/github.com/mem/cobra-context-demo#section-readme)
* [cobra-context-demo/main.go at eec1bd5b08ee162f9cc064d4defe73666f255fac · mem/cobra-context-demo](https://github.com/mem/cobra-context-demo/blob/eec1bd5b08ee/main.go)
* [vgarvardt/grpc-tutorial: Simple gRPC service written in Go with steps to reproduce](https://github.com/vgarvardt/grpc-tutorial)
* [build package - go/build - Go Packages](https://pkg.go.dev/go/build)
* [go - How to build executable with name other than Golang package - Stack Overflow](https://stackoverflow.com/questions/42706246/how-to-build-executable-with-name-other-than-golang-package)
* [Basics tutorial | Go | gRPC](https://grpc.io/docs/languages/go/basics/#client)
* [grpc-go/examples/route\_guide/client/client.go at master · grpc/grpc-go](https://github.com/grpc/grpc-go/blob/master/examples/route_guide/client/client.go)
* [makefile execute another target - Stack Overflow](https://stackoverflow.com/questions/3267145/makefile-execute-another-target)
* [shell - How do I make rm not give an error if a file doesn't exist? - Super User](https://superuser.com/questions/76061/how-do-i-make-rm-not-give-an-error-if-a-file-doesnt-exist)
* [cmd/go: result of 'go build -o' is missing the executable bit, and the resulting file does not execute (despite adding +x) · Issue #33889 · golang/go](https://github.com/golang/go/issues/33889)




# Thought Stream 2023-07-28
* [RabbitMQ: easy to use, flexible messaging and streaming — RabbitMQ](https://rabbitmq.com/)
* [amqp091-go/\_examples/consumer/consumer.go at main · rabbitmq/amqp091-go](https://github.com/rabbitmq/amqp091-go/blob/main/_examples/consumer/consumer.go)
* [6 Top Message Brokers for Modern Applications - Geekflare](https://geekflare.com/top-message-brokers/)
* [Amazon SQS examples using SDK for Go V2 - AWS SDK Code Examples](https://docs.aws.amazon.com/code-library/latest/ug/go_2_sqs_code_examples.html)
* [n8n public REST API | n8n Docs](https://docs.n8n.io/api/)
* [npm | n8n Docs](https://docs.n8n.io/hosting/installation/npm/)
* [Raindrop credentials | n8n Docs](https://docs.n8n.io/integrations/builtin/credentials/raindrop/?utm_source=n8n_app&utm_medium=left_nav_menu&utm_campaign=create_new_credentials_modal)
* [Move Binary Data | n8n Docs](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.movebinarydata/?utm_source=n8n_app&utm_medium=node_settings_modal-credential_link&utm_campaign=n8n-nodes-base.moveBinaryData#4-write-binary-file-node)
* [Markdown | n8n Docs](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.markdown/#markdown-to-html)
* [JSON to Plain Text - Questions - n8n](https://community.n8n.io/t/json-to-plain-text/18436)
* [AWS SNS | n8n Docs](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.awssns/#example-usage)
* [Move Binary Data | n8n Docs](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.movebinarydata/?utm_source=n8n_app&utm_medium=node_settings_modal-credential_link&utm_campaign=n8n-nodes-base.moveBinaryData)
* [How to format date like this? - Questions - n8n](https://community.n8n.io/t/how-to-format-date-like-this/14345/2)
* [after file create n8n - Google Search](https://www.google.com/search?q=after+file+create+n8n&sxsrf=AB5stBg1gpv8Hs14lRxQaAVYrnT2jcja0g%3A1690559010798&ei=IuLDZNikMOzg0PEP_em3oAU&ved=0ahUKEwjYvb2K37GAAxVsMDQIHf30DVQQ4dUDCBA&uact=5&oq=after+file+create+n8n&gs_lp=Egxnd3Mtd2l6LXNlcnAiFWFmdGVyIGZpbGUgY3JlYXRlIG44bjIFECEYoAFItCtQAFiAKnABeAGQAQCYAZkBoAGYEKoBBDE1Lje4AQPIAQD4AQHCAgQQIxgnwgIHECMYigUYJ8ICCBAAGIoFGJECwgITEC4YigUYsQMYgwEYxwEY0QMYQ8ICBxAAGIoFGEPCAgsQABiABBixAxiDAcICCxAuGIoFGLEDGIMBwgILEC4YgAQYxwEY0QPCAgoQABiKBRixAxhDwgIKEC4YigUYsQMYQ8ICBxAuGIoFGEPCAhEQLhiABBixAxiDARjHARjRA8ICChAAGIAEGBQYhwLCAgoQLhixAxiKBRhDwgILEC4YgAQYsQMY1ALCAg0QABiKBRixAxiDARhDwgIIEAAYgAQYsQPCAgUQLhiABMICCxAuGIAEGLEDGIMBwgIFEAAYgATCAgsQLhiABBjHARivAcICFBAuGIAEGJcFGNwEGN4EGOAE2AEBwgIHEC4YgAQYCsICDRAAGIAEGLEDGIMBGArCAgcQABiABBgKwgIGEAAYFhgewgIIEAAYFhgeGArCAggQABgWGB4YD8ICCBAAGIoFGIYDwgIFECEYqwLCAggQIRgWGB4YHeIDBBgAIEGIBgG6BgYIARABGBQ&sclient=gws-wiz-serp#ip=1)
* [aws.iam.User | Pulumi Registry](https://www.pulumi.com/registry/packages/aws/api-docs/iam/user/)