# Docs Zustack CDN

# Performance Test


See our global CDN in action!

```bash
https://tools.keycdn.com/performance?url=https://assets.zustack.com/public/601feaf4-2e90-430d-8823-48076c31d9d1/a5273bbb-3862-43a4-9388-367b60cb0d4c/1a3f0ca3-af43-4d75-aa95-95e76a9fc9d7.webp
```

# Image Optimizer


488 KiB

```bash
https://assets.zustack.com/public/601feaf4-2e90-430d-8823-48076c31d9d1/a5273bbb-3862-43a4-9388-367b60cb0d4c/33aabece-0050-4cd0-bdd7-d32bb6ec9b64.jpg
```


62 KiB

```bash
https://assets.zustack.com/public/601feaf4-2e90-430d-8823-48076c31d9d1/a5273bbb-3862-43a4-9388-367b60cb0d4c/1a3f0ca3-af43-4d75-aa95-95e76a9fc9d7.webp
```


# Getting started

To obtain the API key and App ID, create an app if you haven’t done so yet. 
Then go to the Api Key section and copy the value of the Api Key and the App ID.

# Client side uploads

- `APP_ID`: The ID of your app.
- `SECONDS`: The duration in seconds that the JWT will be valid.
- `JWT`: The JWT signed with your API key. 

```bash
curl -X POST "https://cdn.zustack.com/api/files/generate/signurl/{APP_ID}/{SECONDS}" \
  -H "Authorization: Bearer {JWT}" \
```

This request will return a signed URL that looks like this:

```json
{"url":"https://cdn.zustack.com/api/files/upload/signurl/{APP_ID}/{JWT}"}
```

Our servers will validate that the token is not expired and is signed with your API key.

Once you have the URL, you can upload the file with the following parameters:

- `access`: Set whether the file will be public or private.
- `webp`: Leave blank if you don't want optimization.
- `file`: The file you want to upload.

```bash
curl -X POST "https://cdn.zustack.com/api/files/upload/signurl/{APP_ID}/{JWT}" \
  -H "Content-Type: multipart/form-data" \
  -F "access=public" \
  -F "webp=true" \
  -F "file=@/home/agust/Pictures/neovim.png"
```

After making the request, it will return the following:
```json
{"file-url":"https://assets.zustack.com/path/to/file.webp"}
```

# Sever side uploads

- `APP_ID`: The ID of your app.
- `access`: Set whether the file will be public or private.
- `webp`: Leave blank if you don't want optimization.
- `file`: The file you want to upload.
- `JWT`: The JWT signed with your API key. 

```bash
curl -X POST "https://cdn.zustack.com/api/files/{APP_ID}" \
  -H "Authorization: Bearer {JWT}" \
  -H "Content-Type: multipart/form-data" \
  -F "access=public" \
  -F "webp=true" \
  -F "file=@/home/agust/Pictures/neovim.png"
```

After making the request, it will return the following:
```json
{"file-url":"https://assets.zustack.com/path/to/file.webp"}
```
