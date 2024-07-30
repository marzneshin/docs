---
title: "Webhook notifications"
---

You can set a webhook address and Marzneshin will send the notifications to that address.

the requests will be sent as a post request to the address provided by `WEBHOOK_ADDRESS` with `WEBHOOK_SECRET`
as `x-webhook-secret` in the headers.

Example request sent from Marzneshin:

```
Headers:
Host: 0.0.0.0:9000
User-Agent: python-requests/2.28.1
Accept-Encoding: gzip, deflate
Accept: */*
Connection: keep-alive
x-webhook-secret: something-very-very-secret
Content-Length: 107
Content-Type: application/json

Body:
{"username": "marzneshin_test_user", "action": "user_updated", "enqueued_at": 1680506457.636369, "tries": 0}
```

Different action typs
are: `user_created`, `user_updated`, `user_deleted`, `user_limited`, `user_expired`, `user_disabled`, `user_enabled`
