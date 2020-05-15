---
layout: post
title: Hash Tricks
---
Hash tricks for python and java.

## MD5 in python and java

reference: https://pad.yohdah.com/101/python-vs-java-md5-hexdigest

```python
# the PYTHON way
import sys
from hashlib import md5
for arg in sys.argv[1:]:
    print md5(arg).hexdigest()
```

```java
import java.security.MessageDigest;
import java.math.BigInteger;

class MD5 {
    public String message;
    public MD5( String message ) {
        this.message = message;
    }
    public String hexdigest() throws Exception {
        String hd;
        MessageDigest md5 = MessageDigest.getInstance( "MD5" );
        md5.update( this.message.getBytes() );
        BigInteger hash = new BigInteger( 1, md5.digest() );
        hd = hash.toString(16); // BigInteger strips leading 0's
        while ( hd.length() < 32 ) { hd = "0" + hd; } // pad with leading 0's
        return hd;
    }
    public static void main( String[] args ) throws Exception {
        for ( String message: args ) {
            System.out.println( new MD5( message ).hexdigest() );
        }
    }
}
```
