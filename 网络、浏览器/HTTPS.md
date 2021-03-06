在介绍 HTTPS 之前，先引入两个概念：**对称加密**和**非对称加密**。

1. **`对称加密`**：对称加密在加密和解密的过程中只使用一个密钥，这个密钥叫对称密钥，也叫共享密钥。
2. **`非对称加密`**：非对称加密在加密的过程中使用公开密钥，在解密的过程中使用私有密钥。

HTTPS 采用混合加密机制，将两种加密算法组合使用，充分利用各自的优点。**在交换共享密钥阶段使用非对称加密，在传输报文阶段使用对称加密**。

## HTTPS 解决的问题

HTTPS 很好的解决了 HTTP 的三个缺点（被窃听、被篡改、被伪造），HTTPS 不是一种新的协议，它是 HTTP + SSL 的结合体。

**SSL（Secure Sockets Layer，安全套接层）** 及其继任者 **TLS（Transport Layer Security，传输层安全）** 是为网络通信提供安全及数据完整性的一种安全协议。TLS 与 SSL 在传输层对网络连接进行加密。

HTTPS 改变了通信方式，它由以前的 HTTP => TCP，改为 **HTTP => SSL => TCP**。

- 防监听

  数据是加密的，所以监听到的数据是密文。

- 防伪装

  伪装分客户端伪装和服务器伪装，通信双方携带证书，证书相当于身份证，由第三方颁布，很难伪造。

- 防纂改

  HTTPS 对数据做了摘要，篡改数据会被感知到。

## HTTPS 连接建立过程

- **服务器端需要认证的通信过程**

  ![](http://img-blog.csdn.net/20160812210802573)

  1. 客户端发送请求到服务器
  2. 服务器返回证书和公钥，公钥作为证书的一部分而存在
  3. 客户端验证证书和公钥的有效性，如果有效，则生成共享密钥并使用公钥加密发送到服务器
  4. 服务器使用私钥解密数据，并使用收到的共享密钥加密数据，发送到客户端
  5. 客户端使用共享密钥解密数据
  6. SSL 加密建立

- **客户端认证的通信过程**

  客户端需要认证的过程跟服务器需要认证的过程基本相同，并且少了最开始的两步。这种情况都是证书存储在客户端，并且应用场景比较少，一般金融才用，比如支付宝、银行客户端都需安装证书。

