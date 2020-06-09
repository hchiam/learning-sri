# Learning SRI (Subresource Integrity)

Just one of the things I'm learning. <https://github.com/hchiam/learning>

Make sure that JS from a CDN didn't get hacked or have malicious code injected into it by comparing the code to a hash before running it.

## References

- <https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity>
- <https://www.smashingmagazine.com/2019/04/understanding-subresource-integrity/>

## How to set it up

```bash
cat FILENAME.js | openssl dgst -sha384 -binary | openssl base64 -A
# or
shasum -b -a 384 FILENAME.js | awk '{ print $1 }' | xxd -r -p | base64
```
