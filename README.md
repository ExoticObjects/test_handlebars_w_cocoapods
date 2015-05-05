# test_handlebars_w_cocoapods

This project is a nearly blank XCode project that declares `handlebars-obj` as a dependency in its Podfile. Compilation fails with lots of errors.

- cd to project directory
- Run pod --verbose install
- Open test_handlebars_w_cocoapods.xcworkspace
- Run
- See error log

Unfortunately, I don't know enough about why these errors are happening to fix them. ARC does legitimately forbid a number of things that are happening in handlebars-obc - like Objective-C objects in structs and unions. That would indicate that the fix should come from Handlebars-objc. But, Cocoapods versions 0.35.0 and below compiles this code just fine. However, using cocoapods < 0.35.0 is now unsustainable, as you need > 0.36.0 for Swift support. So it's a conundrum. Hopefully someone will have some ideas...
