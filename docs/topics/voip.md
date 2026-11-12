# voip

[全部主题](../index.md){ .md-button }

<div class="kb-card" markdown="1">

## SIP 中 PRACK 的作用

*未标注* <span class="kb-pill">#voip</span> <span class="kb-pill">#sip</span>

> PRACK 是对临时响应（PR）的确认，保证 101–199 类临时响应的可靠传输。

**要点**

- 临时响应如 `180 Ringing` 需要 PRACK 确认，否则 PR 会被重传
- `100 Trying` 不需要 PRACK
- 最终响应（如 `200 OK`）标志会话建立

</div>

<div class="kb-card" markdown="1">

## RTSP、RTP、RTCP 的分工

*未标注* <span class="kb-pill">#voip</span> <span class="kb-pill">#流媒体</span>

> RTSP 负责发起和终止流媒体，RTP 负责传输音视频数据，RTCP 负责对 RTP 进行控制和同步。

**要点**

- RTSP：实时流协议，控制会话的建立、播放和终止
- RTP：实时传输协议，承载音视频数据
- RTCP：RTP 的控制协议，提供质量反馈和同步信息

</div>

<div class="kb-card" markdown="1">

## SIP 响应状态码速查

*未标注* <span class="kb-pill">#voip</span> <span class="kb-pill">#sip</span>

> SIP 状态码按首位数字分类。

**分类**

- `1xx` 临时响应：`100 Trying`、`180 Ringing`
- `2xx` 成功：`200 OK`
- `3xx` 重定向：`301 Moved Permanently`、`302 Moved Temporarily`
- `4xx` 客户端错误：`400 Bad Request`、`401 Unauthorized`、`403 Forbidden`、`404 Not Found`
- `5xx` 服务器错误、`6xx` 全局失败

</div>
