# Introduction of new features for VS Code debugging

>ruby/debug, which is a replacement for traditional lib/debug.rb standard library has been developed for two years. Also, many improvements are still being made. In this talk, I'll introduce new features to improve the user experience in VS Code debugging. VS Code Debug Visualizer: Would it be helpful if we could see the Active Record object as a table? Debug Visualizer allows you to visualize many objects in many ways, such as bar charts and line charts! Demo: https://www.youtube.com/watch?v=9vLVCrpzlDQ VS Code Record & Replay View: We want to go back to some points when debugging it, don’t we? You can quickly go back and forth between the program by clicking on Record & Replay View! VS Code Trace View: Do you ever want to see what methods have been called until a specific place? You can check the tracing logs if you use Trace View!

## Trace Inspector
- vscode ⇔ vscode extenstion ⇔ ruby/debug
  - extensionとruby/debugの間は、Debug Adaptor Protocol(jsonrpc)で通信してる
