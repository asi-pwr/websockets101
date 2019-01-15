% WebSockets 101
% Michał Zając

# What are WebSockets?

## Two-way communication channel

Using one TCP socket.

## Does it require HTTP?

Technically, no. Practically, yes.

## ????

WebSockets were designed to work over HTTP ports 80 and 443 and to support proxies and other intermediaries.

## Can I use it?

According to https://caniuse.com/#feat=websockets all modern browsers support WebSockets.

# How do WebSockects work?

## HTTP compatibility

WebSockets use HTTP Upgrade header to change the protocol.

## Example request

```
GET /chat HTTP/1.1
Host: server.example.com
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: x3JJHMbDL1EzLkh9GBhXDw==
Sec-WebSocket-Protocol: chat, superchat
Sec-WebSocket-Version: 13
Origin: http://example.com
```

## Example response

```
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: HSmrc0sMlYUkAGmm5OPpG2HaGWk=
Sec-WebSocket-Protocol: chat
```

## Opening handshake - request

1. Method used MUST be `GET`.
2. Request URI must have the same relative or absolute path as the WebSocket URI.
3. Request MUST contain `Host` header which matches the WebSocket URI.
4. Request MUST contain `Connection` header whose value MUST include `Upgrade` token.
5. Request MUST contain `Sec-WebSocket-Key` header whose value MUST be a base64-encoded 16-byte value.
6. Request MUST contain `Sec-WebSocket-Version` header whose value MUST be `13`.

## Opening handshake - response

1. Response request code must be `101 Switching Protocols`.
2. Response MUST contain `Upgrade` header with value being case-insensitive match of `websocket`.
3. Response MUST contain `Connection` header with value matching `Upgrade` case-insensitively.
4. Response MUST contain `Sec-WebSocket-Accept` header with value being base64-encoded SHA-1 of `Sec-WebSocket-Key` with the string `258EAFA5-E914-47DA-95CA-C5AB0DC85B11`

## Further communication

Once the connection is established both client and server can send WebSocket data or text frames back and forth in full-duplex mode.

The data is minimally framed, with a small header followed by payload.

# Further reading

##

#. https://en.wikipedia.org/wiki/WebSocket
#. https://tools.ietf.org/html/rfc6455
#. https://www.websocket.org/
