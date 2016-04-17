## Name

lua-resty-libinjection - Lua FFI wrapper for libinjection

## Status

This library is in active development and is production ready

## Description

This library provides FFI bindings for [libinjection](https://github.com/client9/libinjection/), a SQL/SQLi tokenizer and analyzer.

## Synopsis

```lua
  access_by_lua_block {
    local libinjection = require "resty.libinjection"
    
    -- simple API
    local issqli, fingerprint = libinjection.sql(string)
    
    -- context-specific bindings are also provided
    issql, fingerprint = libinjection.sqli_noquote(string)
    issql, fingerprint = libinjection.sqli_singlequote(string)
    issql, fingerprint = libinjection.sqli_doublequote(string)
  }
```

## Usage

### libinjection.sqli

**syntax**: issqli, fingerprint = libinjection.sqli(string)

Given a string, returns a boolean *issqli* representing if SQLi was detected, and a string *fingerprint* representing the libinjection fingerprint detected. In most cases, this is the preferable option; second-level API bindings noted below may be slightly more efficient in specific contexts.

### libinjection.sqli_noquote(string)

**syntax**: issqli, fingerprint = libinjection.sqli_noquote(string)

Like [libinjection.sqli](libinjectionsqli), in the specific context of an "as-is" string.

### libinjection.sqli_singlequote(string)

**syntax**: issqli, fingerprint = libinjection.sqli_singlequote(string)

Like [libinjection.sqli](libinjectionsqli), in the specific context of a single-quoted (`'`) string.

### libinjection.sqli_doublequote(string)

**syntax**: issqli, fingerprint = libinjection.sqli_doublelequote(string)

Like [libinjection.sqli](libinjectionsqli), in the specific context of a double-quoted (`"`) string.

## License

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program. If not, see http://www.gnu.org/licenses/

## Bugs

Please report bugs by creating a ticket with the GitHub issue tracker.