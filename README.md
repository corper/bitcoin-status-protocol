# Bitcoin status service

Bitcoin status service sends status data of Bitcoin to Bitcoin SV blockchain every hour.

## Sender
Bitcoin status service always send data from address [1LFfrDM27KXeUn1xH9NTknWHexTxqiEcnF](https://bchsvexplorer.com/address/1LFfrDM27KXeUn1xH9NTknWHexTxqiEcnF).  You can tip to this address if you like this service. Tips keep this service alive.

## Data Format
Data is saved in OP_RETURN. Here is a example:
```
status
{
  "version":"0.2.0",
  "timestamp":1549769217,
  "data":{
    "bsv":{
      "price":65.68,
      "tx_num_24h":5765,
      "avg_size_per_blk_24h":825756
    },
    "bch":{
      "price":127.13,
      "tx_num_24h":9903,
      "avg_size_per_blk_24h":65227
    },
    "btc":{
      "price":3663.64,
      "tx_num_24h":288881
      "avg_size_per_blk_24h":1115368
    }
  },
  "source":{
    "price":"https://bitkan.com",
    "tx_num_24h":"https://blockchair.com"
  }
}
```
### Data type
The UTF-8 string `status` is used to identity the data format of the following json object. It is the first section of OP_RETURN data.

For now, there is only one data type.

### Object
The UTF-8 json object string after data type is the second section of OP_RETURN data.

| Field | Type | Description |
| --- | --- | --- |
| version | string | Version of the protocol |
| timestamp | unsigned int | Timestamp when tx broadcasting |
| bsv/bch/btc | object | Name of blockchain and coin which data belongs to |
| price | decimal | Price in USD |
| tx_num_24h | unsigned int | Tx number in latest 144 blocks |
| avg_size_per_blk_24h | unsigned int | Average block size in byte of latest 144 blocks |
| source | object | Data source |

## How to use
You can query or subscribe these data through [bitdb](https://bitdb.network/) or [bitsocket](https://bitsocket.network/).

[Qeury data in latest 10 hours](https://genesis.bitdb.network/query/1FnauZ9aUH2Bex6JzdcV4eNX7oLSSEbxtN/ewogICJ2IjogMywKICAicSI6IHsKICAgICJmaW5kIjogewogICAgICAiaW4uZS5hIjoiMUxGZnJETTI3S1hlVW4xeEg5TlRrbldIZXhUeHFpRWNuRiIsCiAgICAgICJvdXQuYjAiOnsib3AiOjEwNn0KICAgIH0sCiAgICAibGltaXQiOiAxMCwKICAgICJwcm9qZWN0Ijp7Im91dC4kIjoxfQogIH0KfQ==):
```
{
  "v": 3,
  "q": {
    "find": {
      "in.e.a":"1LFfrDM27KXeUn1xH9NTknWHexTxqiEcnF",
      "out.b0":{"op":106}
    },
    "limit": 10,
    "project":{"out.$":1}
  }
}
```
## Applications base on data of bitcoin status service
1. [Bitcoin Status](https://bico.media/edf1f1738e29284129757bc84e2daa2a3f0b92ffb2f256912948b34a2a2614f2.html)

