# Introduction

Shizuku can help normal apps uses system APIs directly with adb/root privileges with a Java process started with app_process.

The name Shizuku comes from [a character](https://danbooru.donmai.us/posts/3553474).

## Why was Shizuku born?

The birth of Shizuku has two main purposes.

1. Provide a convenient way to use system APIs
2. Convenient for the development of some apps that only requires adb permissions

## Shizuku vs. "Old school" method

### "Old school" method

For example, to enable/disable components, some apps that require root privileges execute `pm disable` directly in `su`.

1. Execute `su`
2. Execute `pm disable`
3. (pre-Pie) Start the Java process with app_process ([see here](https://android.googlesource.com/platform/frameworks/base/+/oreo-release/cmds/pm/pm))
4. (Pie+) Execute the native program `cmd` ([see here](https://android.googlesource.com/platform/frameworks/native/+/pie-release/cmds/cmd/))
5. Process the parameters, interact with the system server through the binder, and process the result to output the text result.

Each of the "Execute" means a new process creation, su internally uses sockets to interact with the su daemon, and a lot of time and performance are consumed in such process. (Some poorly designed app will even execute `su` **every time** for each command)

The disadvantages of this type of method are:

1. **Extremely slow**
2. Need to process the text to get the result
3. Features are subject to available commands
4. Even if adb has sufficient permissions, the app requires root privileges to run

### Shizuku method

The Shizuku app will direct the user to run a process (Shizuku service process) using root or adb.

1. When the app process starts, the Shizuku service process sends the binder to the app process.
2. The app interacts with the Shizuku service through the binder, and the Shizuku service process interacts with the system server through the binder.

The advantages of Shizuku are:

1. Minimal extra time and performance consumption
2. It is almost identical to the direct invocation API experience (app developers only need to add a small amount of code)
com.google.firebase.database.DatabaseException: Expected a Map while deserializing, but got a class java.lang.String
	at com.google.firebase.database.core.utilities.encoding.CustomClassMapper.expectMap(CustomClassMapper.java:344)
	at com.google.firebase.database.core.utilities.encoding.CustomClassMapper.deserializeToParameterizedType(CustomClassMapper.java:261)
	at com.google.firebase.database.core.utilities.encoding.CustomClassMapper.deserializeToType(CustomClassMapper.java:176)
	at com.google.firebase.database.core.utilities.encoding.CustomClassMapper.convertToCustomClass(CustomClassMapper.java:101)
	at com.google.firebase.database.DataSnapshot.getValue(DataSnapshot.java:229)
	at com.danzoinj.Login3Activity$6.onChildAdded(Login3Activity.java:350)
	at com.google.firebase.database.core.ChildEventRegistration.fireEvent(ChildEventRegistration.java:79)
	at com.google.firebase.database.core.view.DataEvent.fire(DataEvent.java:63)
	at com.google.firebase.database.core.view.EventRaiser$1.run(EventRaiser.java:55)
	at android.os.Handler.handleCallback(Handler.java:938)
	at android.os.Handler.dispatchMessage(Handler.java:99)
	at android.os.Looper.loop(Looper.java:263)
	at android.app.ActivityThread.main(ActivityThread.java:8299)
	at java.lang.reflect.Method.invoke(Native Method)
