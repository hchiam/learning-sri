# Learning SRI (Subresource Integrity)

Just one of the things I'm learning. <https://github.com/hchiam/learning>

Make sure that JS from a CDN didn't get hacked or have malicious code injected into it by comparing the code to a hash before running it.

Example:

```html
<script
  src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/js/bootstrap.min.js"
  integrity="sha384-OgVRvuATP1z7JjHLkuOU7Xw704+h835Lr+6QL9UvYjZE3Ipu6Tp75j7Bh/kR0JKI"
  crossorigin="anonymous"
></script>
```

Make sure to include _**both**_ `integrity` and [`crossorigin` too](https://shubhamjain.co/til/subresource-integrity-crossorigin).

## References

- <https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity>
- <https://www.smashingmagazine.com/2019/04/understanding-subresource-integrity/>

## How to set it up

```bash
echo sha384-$(cat FILENAME.js | openssl dgst -sha384 -binary | openssl base64 -A)
# or
echo sha384-$(shasum -b -a 384 FILENAME.js | awk '{ print $1 }' | xxd -r -p | base64)
```

Example:

```bash
echo sha384-$(cat index.js | openssl dgst -sha384 -binary | openssl base64 -A)
# or
echo sha384-$(shasum -b -a 384 index.js | awk '{ print $1 }' | xxd -r -p | base64)
```

Either one produces this:

```bash
sha384-A+/1ZBMjbXckmm7EutG5R0nYiAfre+/UZncsGfxQXSpiNIC+gCLZcHfECAkIXMN2
```

And then finally in the HTML:

```html
<script
  src="https://cdn.jsdelivr.net/gh/hchiam/learning-sri@master/index.js"
  integrity="sha384-A+/1ZBMjbXckmm7EutG5R0nYiAfre+/UZncsGfxQXSpiNIC+gCLZcHfECAkIXMN2"
  crossorigin="anonymous"
></script>
```

Which would prevent this:

```html
<script
  src="https://cdn.jsdelivr.net/gh/hchiam/learning-sri@master/index-with-modifications.js"
  integrity="sha384-A+/1ZBMjbXckmm7EutG5R0nYiAfre+/UZncsGfxQXSpiNIC+gCLZcHfECAkIXMN2"
  crossorigin="anonymous"
></script>
```

## Try it out

```bash
open test/index.html
```

Or go to <https://learning-sri.surge.sh>
