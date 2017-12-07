Name
====

lua-resty-libinjection - LuaJIT FFI bindings for libinjection

Status
======

This library is in active development and is production ready

Description
===========

This library provides FFI bindings for [libinjection](https://github.com/client9/libinjection/), a SQL/SQLi and XSS tokenizer and analyzer.

Installation
============

Install this library as you would any other OpenResty lua module. The libinjection shared object file is required to live in your [lua_package_cpath](https://github.com/openresty/lua-nginx-module#lua_package_cpath), so you should symlink or copy the .so file to the appropriate location.

Synopsis
========

```lua
  access_by_lua_block {
    local libinjection = require "resty.libinjection"

    -- simple SQLi API
    local issqli, fingerprint = libinjection.sqli(string)

    -- context-specific bindings are also provided
    issqli, fingerprint = libinjection.sqli_noquote(string)
    issqli, fingerprint = libinjection.sqli_singlequote(string)
    issqli, fingerprint = libinjection.sqli_doublequote(string)

    --simple XSS API
    local isxss = libinjection.xss(string)

    -- context-specific bindings
    isxss = libinjection.xss_data_state(string)
    isxss = libinjection.xss_noquote(string)
    isxss = libinjection.xss_singlequote(string)
    isxss = libinjection.xss_doublequote(string)
    isxss = libinjection.xss_backquote(string)
  }
```

Usage
=====

libinjection.sqli
-----------------

**syntax**: *issqli, fingerprint = libinjection.sqli(string)*

Given a string, returns a boolean *issqli* representing if SQLi was detected, and a string *fingerprint* representing the libinjection fingerprint detected. In most cases, this is the preferable option; second-level API bindings noted below may be slightly more efficient in specific contexts.

libinjection.sqli_noquote
-------------------------

**syntax**: *issqli, fingerprint = libinjection.sqli_noquote(string)*

Like [libinjection.sqli](#libinjectionsqli), in the specific context of an "as-is" string.

libinjection.sqli_singlequote
-----------------------------

**syntax**: *issqli, fingerprint = libinjection.sqli_singlequote(string)*

Like [libinjection.sqli](#libinjectionsqli), in the specific context of a single-quoted (`'`) string.

libinjection.sqli_doublequote
-----------------------------

**syntax**: *issqli, fingerprint = libinjection.sqli_doublelequote(string)*

Like [libinjection.sqli](#libinjectionsqli), in the specific context of a double-quoted (`"`) string.

libinjection.xss
----------------

**syntax**: *isxss = libinjection.xss(string)*

ALPHA version of XSS detector. Given a string, returns a boolean *isxss* denoting if XSS was detected. In most cases, this is the preferable option; second-level API bindings noted below may be slight more efficient in specific contexts.

libinjection.xss_data_state
---------------------------

**syntax**: *isxss = libinjection.xss_data_state(string)*

Like [libinjection.xss](#libinjectionxss), but run with only the DATA_STATE flag.

libinjection.xss_noquote
------------------------

**syntax**: *isxss = libinjection.xss_noquote(string)*

Like [libinjection.xss](#libinjectionxss), but run with only the VALUE_NO_QUOTE flag.

libinjection.xss_singlequote
----------------------------

**syntax**: *isxss = libinjection.xss_singlequote(string)*

Like [libinjection.xss](#libinjectionxss), but run with only the VALUE_SINGLE_QUOTE flag.

libinjection.xss_doublequote
----------------------------

**syntax**: *isxss = libinjection.xss_doublequote(string)*

Like [libinjection.xss](#libinjectionxss), but run with only the VALUE_DOUBLE_QUOTE flag.

libinjection.xss_backquote
--------------------------

**syntax**: *isxss = libinjection.xss_backquote(string)*

Like [libinjection.xss](#libinjectionxss), but run with only the VALUE_BACK_QUOTE flag.

License
=======

Copyright 2017 Robert Paprocki

Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.

3. Neither the name of the copyright holder nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.


Bugs
====

Please report bugs by creating a ticket with the GitHub issue tracker.
