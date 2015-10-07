---
layout: docpage
title: File Endpoint
family: 1.1
---

The `LXFileEndpoint` writes log entries to a specified file.

The File Endpoint is safe to be used in environments featuring concurrency. This [Endpoint][endpoints] will write entries to the file in the order in which they are received without overlapping entries from multiple threads. The File Endpoint does some of its work asynchronously to allow better logging performance.

Because the File Endpoint takes advantage of asynchronous technologies, log entries written to this [Endpoint][endpoints] may appear in the file slightly after execution has moved on. In other words, if your application attempts to create a log entry directly before it crashes, it may not be delivered before the crash occurs. While debugging your application, if the asynchronous nature of this Endpoint is problematic, consider using a [Console Endpoint][ep-console] in addition.

## Usage

### Initialization

The following initializers are available for `LXFileEndpoint`:

{% highlight swift %}
init?(fileURL: NSURL?, minimumLogLevel: LXPriorityLevel = .All, dateFormatter: NSDateFormatter = defaultDateFormatter, entryFormatter: LXEntryFormatter = defaultEntryFormatter)
{% endhighlight %}

LogKit will write log entries to the file specified by `fileURL`. The `fileURL` argument is required. If the specified file cannot be opened, or if `fileURL` evaluates to `nil`, the initializer will fail.

All other arguments are optional and may be excluded. By default, the [Endpoint][endpoints] accepts entries of all [Priority Levels][levels]. `dateFormatter` and `entryFormatter` default to their [default formatters][default-formatting] if they are not provided.

Returns an initialized File Endpoint instance if successful, or `nil` if the file cannot be opened.

{% highlight swift %}
convenience init?(minLogLevel: LXPriorityLevel = .All, dateFormatter: NSDateFormatter = defaultDateFormatter, entryFormatter: LXEntryFormatter = defaultEntryFormatter)
{% endhighlight %}

LogKit will write log entries to the default log file, specified as `{AppSupport}/{bundleID}/logs/log.txt` where `{AppSupport}` is the system-determined Application Support directory, and `{bundleID}` is the host application's `bundleIdentifier` string.

All arguments are optional and may be excluded. By default, the [Endpoint][endpoints] accepts entries of all [Priority Levels][levels]. `dateFormatter` and `entryFormatter` default to their [default formatters][default-formatting] if they are not provided.

Returns an initialized File Endpoint instance if successful, or `nil` if the file cannot be opened.


{% include links.md doc_version=page.family %}