# nginx

[全部主题](../index.md){ .md-button }

<div class="kb-card" markdown="1">

## 配置 Nginx SSL 双向认证

*2025-01-23* <span class="kb-pill">#nginx</span> <span class="kb-pill">#安全</span> <span class="kb-pill">#SSL</span>

> 双向认证要求客户端和服务器都出示证书并互相验证，适合需要限制访问来源的场景。

**步骤**

1. 生成 CA：`openssl genrsa -out ca.key 2048`，再 `openssl req -new -x509 -days 365 -key ca.key -out ca.crt`
2. 分别生成服务器和客户端的私钥与证书请求，并用 CA 签发：`openssl x509 -req ... -CA ca.crt -CAkey ca.key`
3. 在 `server` 中配置 `ssl_certificate`、`ssl_certificate_key`、`ssl_client_certificate`，并设置 `ssl_verify_client on`

**说明**：客户端访问时需要携带自己的证书和私钥。

</div>

<div class="kb-card" markdown="1">

## 反向代理时保持长连接

*未标注* <span class="kb-pill">#nginx</span> <span class="kb-pill">#性能</span>

> 反向代理要保持长连接，需要客户端到 Nginx、Nginx 到后端两段都是长连接。

**步骤**

1. 客户端到 Nginx：默认已开启，可在 `http` 中调整 `keepalive_timeout 120s;` 和 `keepalive_requests 10000;`
2. Nginx 到后端：在 `upstream` 中配置 `keepalive <连接数>;`，并在 `location` 中设置 `proxy_http_version 1.1;` 和 `proxy_set_header Connection "";`

</div>
