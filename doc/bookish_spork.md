

# Module bookish_spork #
* [Description](#description)
* [Data Types](#types)
* [Function Index](#index)
* [Function Details](#functions)

This is the main interface module.

<a name="description"></a>

## Description ##
It provides basic functions for using library

<a name="types"></a>

## Data Types ##




### <a name="type-stub_request_fun">stub_request_fun()</a> ###


<pre><code>
stub_request_fun() = fun((<a href="bookish_spork_request.md#type-t">bookish_spork_request:t()</a>) -&gt; <a href="bookish_spork_response.md#type-response">bookish_spork_response:response()</a>)
</code></pre>

<a name="index"></a>

## Function Index ##


<table width="100%" border="1" cellspacing="0" cellpadding="2" summary="function index"><tr><td valign="top"><a href="#capture_request-0">capture_request/0</a></td><td></td></tr><tr><td valign="top"><a href="#start_server-0">start_server/0</a></td><td>Equivalent to <a href="#start_server-1"><tt>start_server(32002)</tt></a>.</td></tr><tr><td valign="top"><a href="#start_server-1">start_server/1</a></td><td>starts http server on a particular port.</td></tr><tr><td valign="top"><a href="#stop_server-0">stop_server/0</a></td><td>stops http server.</td></tr><tr><td valign="top"><a href="#stub_request-0">stub_request/0</a></td><td>Equivalent to <a href="#stub_request-3"><tt>stub_request(204,
#{&lt;&lt;"Server"&gt;&gt; =&gt; &lt;&lt;"BookishSpork/0.0.1"&gt;&gt;,
&lt;&lt;"Date"&gt;&gt; =&gt; &lt;&lt;"Sat, 28 Apr 2018 05:51:50 GMT"&gt;&gt;},
&lt;&lt;&gt;&gt;)</tt></a>.</td></tr><tr><td valign="top"><a href="#stub_request-1">stub_request/1</a></td><td>Equivalent to <a href="#stub_request-2"><tt>stub_request(Response, 1)</tt></a>.</td></tr><tr><td valign="top"><a href="#stub_request-2">stub_request/2</a></td><td>stub request with fun or particular response.</td></tr></table>


<a name="functions"></a>

## Function Details ##

<a name="capture_request-0"></a>

### capture_request/0 ###

<pre><code>
capture_request() -&gt; {ok, Request::<a href="bookish_spork_request.md#type-t">bookish_spork_request:t()</a>} | {error, Error::term()}
</code></pre>
<br />

<a name="start_server-0"></a>

### start_server/0 ###

<pre><code>
start_server() -&gt; {ok, pid()} | {error, Error::term()}
</code></pre>
<br />

Equivalent to [`start_server(32002)`](#start_server-1).

<a name="start_server-1"></a>

### start_server/1 ###

<pre><code>
start_server(Port::non_neg_integer()) -&gt; {ok, pid()} | {error, Error::term()}
</code></pre>
<br />

starts http server on a particular port

<a name="stop_server-0"></a>

### stop_server/0 ###

<pre><code>
stop_server() -&gt; ok
</code></pre>
<br />

stops http server

<a name="stub_request-0"></a>

### stub_request/0 ###

<pre><code>
stub_request() -&gt; ok
</code></pre>
<br />

Equivalent to [`stub_request(204,#{<<"Server">> => <<"BookishSpork/0.0.1">>,<<"Date">> => <<"Sat, 28 Apr 2018 05:51:50 GMT">>},<<>>)`](#stub_request-3).

<a name="stub_request-1"></a>

### stub_request/1 ###

<pre><code>
stub_request(Response::<a href="#type-stub_request_fun">stub_request_fun()</a> | <a href="bookish_spork_response.md#type-response">bookish_spork_response:response()</a>) -&gt; ok
</code></pre>
<br />

Equivalent to [`stub_request(Response, 1)`](#stub_request-2).

<a name="stub_request-2"></a>

### stub_request/2 ###

<pre><code>
stub_request(Response::<a href="#type-stub_request_fun">stub_request_fun()</a> | <a href="bookish_spork_response.md#type-response">bookish_spork_response:response()</a>, Times::non_neg_integer()) -&gt; ok
</code></pre>
<br />

stub request with fun or particular response

`Response` can be

* either <code>fun((<a href="bookish_spork_request.md#type-t">bookish_spork_request:t()</a>) -> <a href="bookish_spork_response.md#type-response">bookish_spork_response:response()</a>)</code>

* or response data structure <code><a href="bookish_spork_response.md#type-response">bookish_spork_response:response()</a></code>


Example:

```
  bookish_spork:stub_request(fun(Request) ->
      case bookish_spork_request:uri(Request) of
          "/bookish/spork" ->
              [200, [], <<"Hello">>];
          "/admin/sporks" ->
              [403, [], <<"It is not possible here">>]
      end
  end, _Times = 20)
```


