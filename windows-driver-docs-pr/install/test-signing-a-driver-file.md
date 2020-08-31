---
title: 对驱动程序文件进行测试签名
description: 对驱动程序文件进行测试签名
ms.assetid: 3d73d632-e910-43e7-a8fd-c78a11df0206
keywords:
- 测试签名驱动程序包 WDK，驱动程序文件
- 测试签名驱动程序包 WDK，嵌入签名
- 驱动程序文件中的嵌入签名 WDK
- 签名 WDK，embedded
- 数字签名 WDK，embedded
- MakeCert test 证书 WDK
- 测试签名驱动程序文件 WDK
- 商业测试证书 WDK
- 企业 CA 测试证书 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e92686153096cfd358d234c5338a59196c4c54fc
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095449"
---
# <a name="test-signing-a-driver-file"></a>对驱动程序文件进行测试签名

使用 [**SignTool**](../devtest/signtool.md) 将签名嵌入驱动程序文件。

## <a name="using-a-makecert-test-certificate-or-a-commercial-test-certificate-to-embed-a-test-signature-in-a-driver-file"></a>使用 MakeCert 测试证书或商业测试证书将测试签名嵌入驱动程序文件中

使用以下 SignTool 命令通过 [MakeCert 测试证书](makecert-test-certificate.md) 或 [商业测试证书](commercial-test-certificate.md)将签名嵌入驱动程序文件。

```cpp
SignTool sign /v /s TestCertStoreName /n TestCertName /t http://timestamp.digicert.com DriverFileName.sys
```

其中：

- Sign 命令将 SignTool 配置为在驱动程序文件 DriverFileName.sys 中嵌入签名。

- **/V** verbose 选项将 SignTool 配置为打印执行和警告消息。

- **/S** *TestCertStoreName*选项提供包含名为*TestCertName*的测试证书的测试证书存储的名称。

- **/N** *TestCertName*选项提供在名为*TestCertStoreName*的证书存储中安装的测试证书的名称。 测试证书可以是 MakeCert 测试证书，也可以是商业测试证书。

- **/T**  `http://timestamp.digicert.com` 选项提供 DigiCert 提供的公开可用的时间戳服务器的 URL。

- *DriverFileName.sys* 是驱动程序文件的名称。

以下命令演示如何使用 SignTool 对驱动程序文件进行测试签名。 此示例将签名嵌入到 *Toaster.sys*中，该签名位于运行命令的目录下的 *amd64* 子目录中。 测试证书名为 "contoso.com (test) "，它安装在名为 "PrivateCertStore" 的证书存储中。

```cpp
SignTool sign /v /s PrivateCertStore /n contoso.com(test) /t http://timestamp.digicert.com amd64\toaster.sys
```

## <a name="using-an-enterprise-ca-test-certificate-to-embed-a-test-signature-in-a-driver-file"></a>使用企业 CA 测试证书将测试签名嵌入驱动程序文件中

下面的 SignTool 命令假设企业 CA 颁发了测试证书，用于对 [驱动程序包](driver-packages.md)进行签名。 如果 [企业 CA 测试证书](enterprise-ca-test-certificate.md) 是证书存储中提供的唯一测试证书，则可以使用以下命令，其中仅指定 **/a** 选项和驱动程序文件的名称。 在这种情况下，默认情况下，SignTool 将查找并使用企业 CA 测试证书。

如果除了企业 CA 测试证书外，还创建或获取了其他测试证书，则必须使用 SignTool 选项 **/s** 和 **/n** 指定测试证书存储区的名称和测试证书存储中安装的测试证书的名称。

```cpp
SignTool sign /v /a /t http://timestamp.digicert.com DriverFileName.sys
```