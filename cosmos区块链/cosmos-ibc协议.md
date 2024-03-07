## cosmos-ibc协议

* 操作一: Client Creation

* 操作二: Connection Creation

* 操作三: Create Channel

* 操作四: Packet

  包的结构:

  ```golang
  // Packet defines a type that carries data across different chains through IBC
  type Packet struct {
  	Sequence           uint64 `json:"sequence"`            // number corresponds to the order of sends and receives, where a Packet with an earlier sequence number must be sent and received before a Packet with a later sequence number.
  	Timeout            uint64 `json:"timeout"`             // indicates a consensus height on the destination chain after which the Packet will no longer be processed, and will instead count as having timed-out.
  	SourcePort         string `json:"source_port"`         // identifies the port on the sending chain.
  	SourceChannel      string `json:"source_channel"`      // identifies the channel end on the sending chain.
  	DestinationPort    string `json:"destination_port"`    // identifies the port on the receiving chain.
  	DestinationChannel string `json:"destination_channel"` // identifies the channel end on the receiving chain.
  	Data               []byte `json:"data"`                // opaque value which can be defined by the application logic of the associated modules.
  }
  
  ```

  Sequence: 序号, 与包在通道上的发送, 接收序列有关, 通道中的包依据序号大小, 有序发送与接收

  Timeout: 超时, 表示目标链上的区块高度, 当超过该高度以后该包将不会被处理, 并会将其视为已超时

  SourcePort: 源端口, 发送链上的端口

  SourceChannel: 源通道, 发送链上的通道

  DestinationPort: 目标端口, 目标链链上的端口

  DestinationChannel: 目标通道, 目标链上的通道

  Data: 数据, 数据与应用逻辑关联的模块相关
  
