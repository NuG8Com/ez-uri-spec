# ez-uri-spec

> 只是他用 `http://` ，你用 `ez://` 給機器人用。  
> **資料減重90%，解析速度快60,000倍。**

**Status**: Submitted to IANA as #1454153 on 2026-04-15. Pending registration.

## Specification

```
ez-URI    = "ez://" host [ "/" path ] [ "?" query ]
host      = 1*( unreserved / sub-delims )
path      = 1*( unreserved / sub-delims / "/" )
query     = *( unreserved / sub-delims / "=" / "&" )
```

## Security

1. TLS recommended when used over networks.
2. Devices send-only to save power. No response expected.  
3. Use `ts` timestamp to prevent replay attacks.

## Example

See `examples/iot-location.md`
