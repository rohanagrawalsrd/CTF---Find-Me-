Find Me If You Can – JWT nbf Challenge Writeup

Find Me If You Can is a web exploitation challenge that focuses on understanding and abusing JSON Web Tokens (JWT), specifically the nbf (Not Before) claim. The application restricts access to protected resources until a future timestamp, but this restriction can be bypassed by modifying the JWT payload.

Step 1: Extract the JWT Payload

The provided JWT token is split into three parts separated by dots (.). The middle portion of the token is extracted, as it represents the Base64-encoded payload containing the JWT claims.

Step 2: Decode and Modify the nbf Claim

The extracted payload is pasted into a Base64 decoder and decoded to reveal the JSON structure. The nbf claim is identified, which specifies the timestamp before which the token is considered invalid. This value is modified to 0, effectively removing the time-based restriction and allowing immediate access.

Step 3: Re-encode the Modified Payload

After editing the payload, it is re-encoded into Base64 format. URL-safe Base64 encoding is enabled to ensure compatibility with JWT standards.

Step 4: Reconstruct the JWT

The original payload section of the JWT is replaced with the newly encoded payload, while keeping the header and signature unchanged. This results in a modified but still syntactically valid JWT.

Step 5: Inject the Modified Token

The ModHeader browser extension is installed and enabled. An Authorization header is added with the value Bearer <modified_jwt>, ensuring that all outgoing requests include the modified token.

Step 6: Access the Flag Endpoint

With the modified JWT injected, the /flag endpoint is accessed. Since the nbf restriction has been bypassed, the server accepts the token and returns the flag.

Flag

LNMHACKS{jwt_nbf_time_travel}
