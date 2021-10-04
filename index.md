## Android Security

Android requires that all APKs be digitally signed with a certificate at the build time and it will be verified using the PackageManager at the boot time. Application signing allows developers to identify the author of the application and to update their application without creating complicated interfaces and permissions. Every application that is run on the Android platform must be signed by the developer. The document is intended for the audience who would like to sign the build with keys and use a verifier to unparse while bootup.

### APK Signing schemes

 Android supports three application signing schemes:

   - v1 scheme: based on JAR signing
   - v2 scheme: APK Signature Scheme v2, which was introduced in Android 7.0.
   - v3 scheme: APK Signature Scheme v3, which was introduced in Android 9.

For maximum compatibility, sign applications with all schemes, first with v1, then v2, and then v3. Android 7.0+ and newer devices install apps signed with v2+ schemes more quickly than those signed only with v1 scheme. Older Android platforms ignore v2+ signatures and thus need apps to contain v1 signatures. 

### The following standard test keys are currently included in the Android builds

```
testkey -- a generic key for packages that do not otherwise specify a key.
platform -- a test key for packages that are part of the core platform.
shared -- a test key for things that are shared in the home/contacts process.
media -- a test key for packages that are part of the media/download system.
```
The above key can be generated from the development/tools/make_key project from the Android sources.

### Sample Key generation
The following commands were used to generate the test key pairs:

```
  development/tools/make_key testkey  '/C=US/ST=California/L=Mountain View/O=Android/OU=Android/CN=Android/emailAddress=android@android.com'
  development/tools/make_key platform '/C=US/ST=California/L=Mountain View/O=Android/OU=Android/CN=Android/emailAddress=android@android.com'
  development/tools/make_key shared   '/C=US/ST=California/L=Mountain View/O=Android/OU=Android/CN=Android/emailAddress=android@android.com'
  development/tools/make_key media    '/C=US/ST=California/L=Mountain View/O=Android/OU=Android/CN=Android/emailAddress=android@android.com'
```
Note: Add the third argument as "ec" to get the ecc version of the corresponding keys.

### Verification

In Android 7.0 and later, APKs can be verified according to the APK Signature Scheme V3, V2 or JAR signing (V1 scheme). Older platforms ignore V3, V2 signatures and only verify V1 signatures. 

![](https://source.android.com/security/images/apk-v2-validation.png)


To Know more about the Verifier schemes, here are the links,
[V3](https://source.android.com/security/apksigning/v3), [V2](https://source.android.com/security/apksigning/v2)

Hence, the PacakgeManager will parse the apk signer block and verify it against the Publickey.


