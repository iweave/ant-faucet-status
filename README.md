# ANT Faucet status page

A temporary static maintenance page for [ant.xd7.org](https://ant.xd7.org). The automated faucet is offline because its forum-based eligibility verification service is no longer available.

This repository does **not** contain or run the original faucet, wallet, token distribution API, or credentials.

## Deploy with Coolify

1. Create a **new resource → Application** in Coolify and select the GitHub repository `iweave/ant-faucet-status`. Alternatively, for a public repository, use `https://github.com/iweave/ant-faucet-status.git`.
2. Select **Dockerfile** as the build pack. The Dockerfile is at the repository root.
3. Set the application's internal port to **80**.
4. Configure the domain **https://ant.xd7.org** and enable HTTPS/Let's Encrypt.
5. Deploy after pointing the DNS A record at your Coolify server's public IPv4 address. Remove or update stale AAAA records if IPv6 isn't configured.
6. Verify that the homepage displays the maintenance notice and an unrelated path such as `/api/claim` returns HTTP 404.

No environment variables, database, persistent storage, or wallet secrets are required.

## Local test

```sh
docker build -t ant-faucet-status .
docker run --rm -p 8080:80 ant-faucet-status
```

Visit [http://localhost:8080](http://localhost:8080) and stop with Ctrl+C.

To update the notice, edit `index.html`, commit, and redeploy. Restore the original service only after a separate security review.
