---
title: Content Negotiation
draft: false
publish: true
tags:
  - 🌱
date: 2024-09-11
---
Two patterns for response content

- **Proactive content negotiation (server driven negotiation)** In this case, the server is responsible for selecting the most convenient representation based on knowledge about the user agent. This knowledge may include explicit content negotiation headers (Accept, Accept-Encoding, Accept-Charset, Accept-Language) or implicit characteristics such as parts of the User-Agent header or network address.
- **Reactive content negotiation (agent driven negotiation)** With this approach, the user agent selects the best fitting representation after receiving an initial response. Instead of sending an initial representation, the server may send a list of available representations with response code 300 (multiple choices) or 406 (not acceptable). Based on this information, the user agent performs another request with the selected representation.

We can identify the following headers within the content negotiation standard:

- **Accept**: The header can be used to specify preferences of message content media type. When sending in a request, it specifies user agent preferences to response content. When sending an int response, it specifies server preferences to request content in subsequent requests.
- **Accept-Charset**: According to RFC guidelines, has been deprecated and should be avoided if possible, however, before its deprecation, it was used to indicate preferences for charset. Wildcard can be used to indicate every charset that is not mentioned elsewhere in the field.
- **Accept-Encoding**: This header serves the purpose of expressing preferences for content coding. This header allows user agents to indicate the types of content coding they find acceptable in the response while also enabling servers to specify the preferred content coding for subsequent requests. An identity token is used as a synonym for no encoding.
- **Accept-Language**: enables user agents to express preferred natural languages for responses. It uses language tags to represent these preferences, allowing users to prioritize languages. Language tags can have associated quality values reflecting user preferences.
- **Vary**: is the response header that describes which parts of a request, other than the method and target, affect how the server picks the response representation. It can be a wildcard * or a list of request field names that might have played a role in picking the response representation.

Links:

[Content Negotiation in Practice](https://softwaremill.com/content-negotiation-in-practice/)
[MDN Content Negotiation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation)