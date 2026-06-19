> ⚠️ **Official Spec v1.1.0**: Identical to IANA Ticket #1454153 submission. Provisional registration.

# ez-uri-spec

## 1. Scheme Name
ez

## 2. Status
Provisional

## 3. URI Scheme Syntax
The complete ABNF definition is as follows:
```
ez-URI = "ez" ":" hier-part [ "?" query ] [ "#" fragment ]
hier-part = "//" authority path-abempty
authority = [ userinfo "@" ] host [ ":" port ]
userinfo = *( unreserved / pct-encoded / sub-delims / ":" )
host = IP-literal / IPv4address / reg-name
port = *DIGIT
path-abempty = *( "/" segment )
segment = *pchar
pchar = unreserved / pct-encoded / sub-delims / ":" / "@"
query = *( pchar / "/" / "?" )
fragment = *( pchar / "/" / "?" )
```
**Additional syntax and validation considerations:**

- Per RFC 3986 Section 3.2, when the "//" authority delimiter is present, the host component MUST be present; therefore, a URI of the form `ez://:1618/path` is syntactically invalid. [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986)
- The userinfo component is OPTIONAL. If used, it is intended only for identification data. Plaintext passwords or other secrets in userinfo are NOT RECOMMENDED. [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986)
- The query and fragment components are OPTIONAL. Their semantics are scheme-specific and are defined by the implementing protocol or application profile.
- Implementations MUST validate ez URIs against the syntax defined in this specification before processing them. [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986)
- Characters outside the permitted RFC 3986 grammar MUST be percent-encoded. In particular, the `#` character is only valid as the fragment delimiter unless percent-encoded within another component. [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986)
- For interoperability and defensive processing, implementations MAY impose an overall URI length limit. A recommended initial implementation limit is 128 octets. Any such limit is an implementation constraint and does not alter the normative syntax of the scheme.
- For local deployments, implementations MAY use `localhost` where a loopback-resolved authority is intended. [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986)

**Example URIs:**
- `ez://localhost:1618/task/123`
- `ez://localhost/inference/gpt-oss-120b`
- `ez://192.168.1.45:1618/execute/task-847`
- `ez://gpu-cluster-01/job/abc/status`
- ## 4. URI Scheme Semantics
The "ez" URI scheme identifies addressable resources and service endpoints within distributed compute, task scheduling, and inference systems, including compute tasks, job status resources, scheduling interfaces, execution nodes, and result resources. [RFC7595](https://datatracker.ietf.org/doc/html/rfc7595)

The scheme is intended to provide hardware-agnostic resource identification across heterogeneous compute environments. It allows upper-layer applications and schedulers to refer to resources using a consistent naming model without embedding vendor-specific or architecture-specific semantics in the URI itself. [RFC7595](https://datatracker.ietf.org/doc/html/rfc7595)

Within an ez URI, the authority identifies the hosting service endpoint or scheduler, and the hierarchical path identifies a resource within that service. The detailed interpretation of path segments, query parameters, and fragments is defined by implementations or future protocol specifications layered above the URI scheme.

The scheme itself does not mandate a particular transport protocol, name-resolution mechanism, routing algorithm, or execution model. In particular, syntax validation of an ez URI does not require DNS recursion; host interpretation is delegated to the relevant deployment environment or underlying protocol binding.

## 5. Encoding Considerations
- Non-ASCII characters MUST be encoded using UTF-8 and then percent-encoded as required by RFC 3986. [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986)
- Reserved characters appearing outside their delimiter roles MUST be percent-encoded in accordance with RFC 3986. [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986)
- The scheme name `ez` is composed of lowercase ASCII letters and conforms to the URI scheme naming guidance in RFC 7595. [RFC7595](https://datatracker.ietf.org/doc/html/rfc7595)

## 6. Applications and Protocols Using This Scheme
The ez scheme is intended for use by systems such as:
- Distributed GPU and accelerator scheduling systems
- Heterogeneous compute orchestration platforms
- AI inference and training task coordination systems
- Resource-oriented control planes for distributed execution environments

Formal protocol profiles and implementation specifications are expected to be documented as part of the transition to Permanent registration. [RFC7595](https://datatracker.ietf.org/doc/html/rfc7595)

## 7. Interoperability Considerations
The scheme is designed for cross-vendor and cross-architecture interoperability. [RFC7595](https://datatracker.ietf.org/doc/html/rfc7595)

- No vendor-specific or hardware-specific semantics are embedded in the scheme syntax. [RFC7595](https://datatracker.ietf.org/doc/html/rfc7595)
- The syntax is based on RFC 3986 generic URI components, allowing use with existing URI parsers and tooling that support scheme-specific validation. [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986)
- Interoperability is expected to occur primarily at the protocol and application layers above the URI syntax itself. [RFC7595](https://datatracker.ietf.org/doc/html/rfc7595)

**Illustrative use case: distributed AI inference scheduling**

1. A client submits an inference request using `ez://localhost:1618/inference/gpt-oss-120b`.
2. A scheduler interprets that URI as identifying an inference resource or service endpoint.
3. The scheduler routes the request to an appropriate execution node according to deployment-specific policy.
4. The execution environment returns or exposes a result resource such as `ez://192.168.1.45:1618/result/task-847`.

This example is illustrative only and does not define mandatory protocol behavior for all implementations. [RFC7595](https://datatracker.ietf.org/doc/html/rfc7595)

## 8. Port Considerations
The ez scheme does not require a universal default port as part of its normative syntax definition.

Implementations and protocol profiles MAY define a default port for operational convenience. One anticipated deployment convention is port 1618, which lies within the IANA User Port range. However, any such default is deployment-specific unless and until defined by a formal protocol specification. [RFC7595](https://datatracker.ietf.org/doc/html/rfc7595)

## 9. Security Considerations
- The ez scheme does not itself provide confidentiality, integrity, authentication, or authorization. Such properties MUST be provided by the underlying transport, application protocol, or deployment environment as appropriate. [RFC7595](https://datatracker.ietf.org/doc/html/rfc7595)
- Plaintext credentials or other secrets MUST NOT be conveyed in userinfo, path, or query components. [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986)
- Implementations MUST validate and sanitize ez URIs before use in order to reduce the risk of injection, path confusion, traversal, resource exhaustion, or other malformed-input attacks. [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986)
- Implementations SHOULD impose reasonable bounds on URI length and parsing resource consumption.
- General security considerations from RFC 3986 apply. [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986)

## 10. Contact Information
Name: KuoChun Fang
Email: RoyFang@M-Commerce.com
Organization: M-Commerce.com
Date: Sun, 14 June 2026

## 11. Change Controller
Name: KuoChun Fang
Email: RoyFang@M-Commerce.com
Organization: M-Commerce.com
Date: Sun, 14 June 2026

For this provisional registration, the above contact is authorized to update and modify the registration record.

## 12. Transition Plan from Provisional to Permanent Status
A request for transition to Permanent status will be submitted within 24 months of provisional registration approval. The submission is expected to include:
- Evidence of implementation and deployment experience
- Interoperability results across multiple implementations
- A complete Internet-Draft or RFC specification for the ez URI scheme and related protocol bindings
- Community feedback and review outcomes

This transition plan is consistent with the staged registration model described in RFC 7595. [RFC7595](https://datatracker.ietf.org/doc/html/rfc7595)

## 13. References
[RFC3986] Berners-Lee, T., Fielding, R., and L. Masinter, "Uniform Resource Identifier (URI): Generic Syntax", STD 66, RFC 3986, January 2005. [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986)

[RFC7595] Thaler, D., Ed., Hansen, T., and M. Mealling, "Guidelines and Registration Procedures for URI Schemes", BCP 35, RFC 7595, June 2015. [RFC7595](https://datatracker.ietf.org/doc/html/rfc7595)
