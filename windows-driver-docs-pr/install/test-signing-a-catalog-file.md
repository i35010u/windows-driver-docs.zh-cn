---
title: 对目录文件进行测试签名
description: 对目录文件进行测试签名
ms.assetid: a6397f8f-e5f1-4ce2-af7b-a7846fa30bc8
keywords:
- 目录文件 WDK 驱动程序签名, 测试签名
- 测试签名目录文件 WDK
- 测试签名驱动程序包 WDK, 编录文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70caf48f50cadf12d53ebc642c77e01ad8f60923
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025347"
---
# <a name="test-signing-a-catalog-file"></a>对目录文件进行测试签名


创建并验证[驱动程序包的](driver-packages.md) [目录文件](catalog-files.md)后, 请按照以下主题中所述, 使用[**SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)对编录文件进行测试签名:

[使用 MakeCert 测试证书或商业测试证书对驱动程序包的目录文件进行测试签名](#using-a-makecert-test-certificate-or-commercial-test-certificate-to-te)

[使用企业 CA 测试证书对驱动程序包的目录文件进行测试签名](#using-an-enterprise-ca-test-certificate-to-test-sign-a-driver-package-)

### <a href="" id="using-a-makecert-test-certificate-or-commercial-test-certificate-to-te"></a>使用 MakeCert 测试证书或商业测试证书对驱动程序包的目录文件进行测试签名

使用以下 SignTool 命令通过[MakeCert 测试证书](makecert-test-certificate.md)或[商业测试证书](commercial-test-certificate.md)对[编录文件](catalog-files.md)进行签名:

```cpp
SignTool sign /v /s TestCertStoreName /n TestCertName /t http://timestamp.digicert.com CatalogFileName.cat
```

其中：

-   **Sign**命令将 SignTool 配置为对名为*CatalogFileName.cat*的[目录文件](catalog-files.md)进行签名。

-   **/V** verbose 选项将 SignTool 配置为打印执行和警告消息。

-   **/S** *TestCertStoreName*选项提供包含名为*TestCertName*的测试证书的测试证书存储的名称。

-   **/N** *TestCertName*选项提供在名为*TestCertStoreName*的证书存储中安装的测试证书的名称。 测试证书可以是 MakeCert 测试证书, 也可以是商业测试证书。

-    */T http://timestamp.digicert.com* 选项提供 DigiCert 提供的公开可用的时间戳服务器的 URL。

-   *CatalogFileName.cat*是[目录文件](catalog-files.md)的名称。

以下命令演示如何使用 SignTool 对[驱动程序包的](driver-packages.md)目录文件进行测试签名。 此示例对目录文件*Tstamd64.cat*进行签名, 该文件位于运行命令的同一目录中。 测试证书名为 "contoso .com (test)", 该证书安装在名为 "PrivateCertStore" 的证书存储中。

```cpp
SignTool sign /v /s PrivateCertStore /n contoso.com(test) /t http://timestamp.digicert.com tstamd64.cat
```

### <a href="" id="using-an-enterprise-ca-test-certificate-to-test-sign-a-driver-package-"></a>使用企业 CA 测试证书对驱动程序包的目录文件进行测试签名

下面的 SignTool 命令假设企业 CA 颁发了测试证书, 用于对[驱动程序包](driver-packages.md)进行签名。 如果[企业 CA 测试证书](enterprise-ca-test-certificate.md)是证书存储中提供的唯一测试证书, 则可以使用以下命令, 其中仅指定 **/a**选项和[编录文件](catalog-files.md)的名称。 在这种情况下, 默认情况下, SignTool 将查找并使用企业 CA 测试证书。

如果除了企业 CA 测试证书外, 还创建或获取了其他测试证书, 则必须使用 SignTool 选项 **/s**和 **/n**指定测试证书存储的名称和测试证书的名称。安装在测试证书存储区中。

```cpp
SignTool sign /v /a /t http://timestamp.digicert.com CatalogFileName.cat
```

 

 





