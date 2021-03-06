{% case include.family %}

{% else %}
> The {{ include.endpoint_type }} Endpoint is safe to be used in environments featuring concurrency. This [Endpoint][endpoints] does some of its work asynchronously to allow better logging performance. Because the {{ include.endpoint_type }} Endpoint takes advantage of asynchronous technologies, [Log Entries][entries] written to this [Endpoint][endpoints] may not appear until slightly after execution has moved on. In other words, if your application attempts to create a Log Entry directly before it crashes, it may not be delivered before the crash occurs. While debugging your application, if the asynchronous nature of this Endpoint is problematic, consider using a synchronous [Console Endpoint][ep-console] in addition.

{% endcase %}
