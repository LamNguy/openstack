```
OS_TOKEN="gAAAAABfSHiOBMc96nOkvQw1eofzCib1IqyiK11_ohmZawZR_k2OZ6u-FVdLVfP7oiKorltCFbGXYxdjQnFkQLuqkeHzy0xwkoOrtIBF5OTI0Te4KrN40gCnR-cPLjtSgmNUX7z4WzViBeagdcmyC_E1TNU5RUCO6qMyDLZA2JASC0X6-gkwz1A"
PRIOR_ROLE_ID="2d25a4b534fd488893347abca452c369"
IMPLIES_ROLE_ID="64f808eaef9041fa93f0745651527a17"
curl -s \
  -X PUT \
  -H "X-Auth-Token: $OS_TOKEN" \
  "http://192.168.0.105:5000/v3/roles/$PRIOR_ROLE_ID/implies/$IMPLIES_ROLE_ID" | python -mjson.tool
```

-H --header : extra header to include
-s : silient mode \
-X --request : PUT , HEAD , GET , HEAD  \
-i --include : include header response \
