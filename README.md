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
