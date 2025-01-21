## sing-box下载
 
[sing-box地址](https://github.com/SagerNet/sing-box)


## 根据json生成二进制规则文件
```sh

./sing-box rule-set compile  --output ./cn.srs  cn.json

```
## 配置文件(config.json)内容

```json
{
    "inbounds": [
        {
            "type": "mixed",
            "listen": "::",
            "listen_port": 10000
        }
    ],
    "outbounds": [
        {
    	       "tag": "🇨🇳 直连域名",
            "type": "direct",
        },
        {
            "tag":"代理",
            "type": "vmess",
            "server": "",
            "server_port": 31271,
            "uuid": "",
            "security": "aes-128-gcm",
            "alter_id": 0,
            "packet_encoding": "packetaddr",
            "transport": {
                "type": "ws",
                "path": "",
                "max_early_data": 2048,
                "early_data_header_name": "Sec-WebSocket-Protocol"
            }
        }
    ],
    "route": {
      "rules": [ 
      		{ 
      		 "rule_set": [ "cn" ], 
      		 "outbound": "🇨🇳 直连域名" 
      		},
      		{
		        "outbound": "代理"
	       }
      ],
      "rule_set": [
      {
      "tag": "cn",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/EUForest/sing-box-rules/refs/heads/main/cn.srs"
      }
    ] 
  }
}
```

## 运行客户端
```sh
./sing-box run -c config.json


```
