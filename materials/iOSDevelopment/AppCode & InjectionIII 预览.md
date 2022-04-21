# AppCode + InjectionIII 预览 配置一览

[toc]

## AppCode设置预览方法：

参考链接：https://www.jetbrains.com/help/objc/create-a-swiftui-application.html#interactive_preview

1. AppStore下载 InjectionIII 并启动

2. 添加 `-Xlinker -interposable` 到 project build settings (cmd + ;) -- Other Linker Flags

3. 添加构造器到应用文件

   ```
   import SwiftUI
   @main
   struct iOSConferencesApp: App {
       // Add this method
       init() {
           #if DEBUG
           var injectionBundlePath = "/Applications/InjectionIII.app/Contents/Resources"
           #if targetEnvironment(macCatalyst)
           injectionBundlePath = "\(injectionBundlePath)/macOSInjection.bundle"
           #elseif os(iOS)
           injectionBundlePath = "\(injectionBundlePath)/iOSInjection.bundle"
           #endif
           Bundle(path: injectionBundlePath)?.load()
           #endif
       }
       var body: some Scene {
           WindowGroup {
               ContentView()
           }
       }
   }
   ```

4. 添加方法到预览的类

   ```
   class ContentView_Previews: PreviewProvider {
       static var previews: some View {
           ContentView()
       }
   
   #if DEBUG
       @objc class func injected() {
           let windowScene = UIApplication.shared.connectedScenes.first as? UIWindowScene
           windowScene?.windows.first?.rootViewController =
                   UIHostingController(rootView: ContentView())
       }
   #endif
   }
   ```

5. 需要cmd + s 保存修改的代码才会有变化，如果要设置自动保存：If you don't want to save changes manually to update the preview, go to Preferences | Appearance & Behavior | System Settings | Autosave, select the Save files automatically if application is idle for … sec checkbox, and set its value to 1.

6. 痛点：每个项目都需要设置一遍。（可以通过live template减少工作量）



## Live Template 新建view

定义 $FILE$    fileNameWithoutExtension()

```
import SwiftUI

struct $FILE$: View {
    var body: some View {
        Text("hello world")
    }
}

class $FILE$_Previews: PreviewProvider {
    #if DEBUG
    @objc class func injected() {
        let windowScene = UIApplication.shared.connectedScenes.first as? UIWindowScene
        windowScene?.windows.first?.rootViewController =
                UIHostingController(rootView: $FILE$())
    }
    #endif

    static var previews: some View {
        $FILE$()
    }
}
```
