
# Embed your Hub into an existing website

There are two methods that will allow you to embed your Hub into an existing website. If you want
to host your published Hub on Stoplight's servers, you will need to set up a reverse proxy. If you want
your Hub to live alongside your website's files, you will need to download your Hub's static assets and
upload them with your website.

## Setting up a base path

Your base path will determine the path to your Hub's landing page. For example if you want your Hub
to be served from `https://example.com/docs/api` then you would set your base path to `/docs/api`.

1. Head to your Stoplight Next project.
2. Open the domains panel and pick custom domain (ex. `https://example.com`).
3. On the publish panel, scroll down to "Advanced" and input your base path (ex: `/docs/api`).
4. At the top of the publish panel, click the "Build & Publish".

![Self-hosted hub directory example](/assets/images/setting-hub-base-path.png)

## Example of self hosting

If you want to host your Hub on the same servers as your website's files, you will need to download
your Hub's static asset files and save them with the rest of your website's files.

1. Read our docs on [Download Static HTML & CSS
](https://docs.stoplight.io/documentation/download-static-html) and complete the steps until you have
your static Hub files.
2. Locate the directory that contains your website's files. (ex. `~/Documents/my-website`)
3. Copy all of the files and folders from your unzipped Hub download and move them to your website's
directory. (ex. Move `~/Downloads/hub-files/...` to `~/Downloads/my-website/...` )
4. Now upload your website's directoy as normal.

This is how your website directory might look:

![Self-hosted hub directory example](/assets/images/example-website.png)

## Example of reverse proxying with AWS API Gateway

1. Go to API Gateway service and create a new API
2. Create a path for `GET /` and `GET /{proxy+}` that proxies to your website.
3. Create a path for `GET /your-base-path` and `GET /your-base-path/{proxy+}` that proxies to `ingress.docs.stoplight/your-base-path` and `ingress.docs.stoplight/your-base-path/{proxy}`
4. Add static headers `Accept-Encoding: 'indentify'` and `Host: your-website.com` to the proxied requests.
5. Deploy your API.
6. Go to the Certificate Manager service and **request a public certificate** for your website's domain.
7. Go back to the API Gateway service - Custom Domain Names section.
8. Add your website's domain and select your ACM certificate.
9. Go to your DNS provider and point your domain at your deployed API.

## Limitations

* Any authentication will need to be handled by your website or the reverse proxy.
* Do not include `/index.html` in your browser when loading your Hub.
