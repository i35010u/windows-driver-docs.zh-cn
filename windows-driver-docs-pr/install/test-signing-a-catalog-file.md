---
title: 对目录文件进行测试签名
description: 对目录文件进行测试签名
ms.assetid: a6397f8f-e5f1-4ce2-af7b-a7846fa30bc8
keywords:
- 目录文件 WDK 驱动程序签名，测试签名
- 测试签名目录文件 WDK
- 测试签名驱动程序包 WDK，目录文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b235ab765e83ccbb2ac4b8e991efc7b87ead6a9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377235"
---
# <a name="test-signing-a-catalog-file"></a>对目录文件进行测试签名


创建并验证后[驱动程序包](driver-packages.md) [编录文件](catalog-files.md)，使用[ **SignTool** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)测试签名目录文件中所述以下主题：

[使用 MakeCert 测试证书或商业测试证书，对测试签名驱动程序包的目录文件](#using-a-makecert-test-certificate-or-commercial-test-certificate-to-te)

[使用企业 CA 测试证书对测试签名驱动程序包的目录文件](#using-an-enterprise-ca-test-certificate-to-test-sign-a-driver-package-)

### <a href="" id="using-a-makecert-test-certificate-or-commercial-test-certificate-to-te"></a> 使用 MakeCert 测试证书或商用测试证书对测试签名驱动程序包的目录文件

使用以下 SignTool 命令进行签名[编录文件](catalog-files.md)通过使用[MakeCert 测试证书](makecert-test-certificate.md)或[商业测试证书](commercial-test-certificate.md):

```cpp
SignTool sign /v /s TestCertStoreName /n TestCertName /t http://timestamp.verisign.com/scripts/timstamp.dll CatalogFileName.cat
```

其中：

-   **符号**命令将配置进行签名的 SignTool[编录文件](catalog-files.md)命名为*CatalogFileName.cat*。

-   **/V**详细选项配置 SignTool 打印执行消息和警告消息。

-   **/S** *TestCertStoreName*选项提供包含名为的测试证书的测试证书存储区的名称*TestCertName*。

-   **/N** *TestCertName*选项提供名为的证书存储中安装的测试证书的名称*TestCertStoreName*。 MakeCert 测试证书或商业测试证书，可以是测试证书。

-   **/T**  *http://timestamp.verisign.com/scripts/timstamp.dll* 选项提供 VeriSign 提供的公开可用的时间戳服务器的 URL。

-   *CatalogFileName.cat*的名称[编录文件](catalog-files.md)。

下面的命令演示如何对测试签名使用 SignTool[驱动程序包的](driver-packages.md)目录文件。 此示例对编录文件进行签名*Tstamd64.cat*，这是在其中运行该命令的相同目录中。 测试证书的名称为"contoso.com(test)，"安装名为"PrivateCertStore。"的证书存储中

```cpp
SignTool sign /v /s PrivateCertStore /n contoso.com(test) /t http://timestamp.verisign.com/scripts/timstamp.dll tstamd64.cat
```

### <a href="" id="using-an-enterprise-ca-test-certificate-to-test-sign-a-driver-package-"></a> 使用企业 CA 测试证书对测试签名驱动程序包的目录文件

以下 SignTool 命令假定，企业 CA 颁发测试登录到在你使用的测试证书[驱动程序包](driver-packages.md)。 如果[企业 CA 测试证书](enterprise-ca-test-certificate.md)是唯一的测试证书位于你的证书存储，可以使用以下命令仅指定其中 **/a**选项以及的名称[编录文件](catalog-files.md)。 在这种情况下，SignTool 将找到并默认情况下使用企业 CA 的测试证书。

如果已创建或获取除了企业 CA 测试证书的其他测试证书，则必须使用 SignTool 选项 **/s**并 **/n**指定测试证书存储区的名称和安装测试证书存储区中的测试证书的名称。

```cpp
SignTool sign /v /a /t http://timestamp.verisign.com/scripts/timstamp.dll CatalogFileName.cat
```

 

 





