---
title: 对驱动程序文件进行测试签名
description: 对驱动程序文件进行测试签名
ms.assetid: 3d73d632-e910-43e7-a8fd-c78a11df0206
keywords:
- 测试签名驱动程序包 WDK，驱动程序文件
- 测试签名驱动程序包 WDK，嵌入签名
- 驱动程序文件 WDK 中的嵌入式的签名
- 签名 WDK 嵌入
- 数字签名 WDK 嵌入
- MakeCert 测试证书 WDK
- 测试签名驱动程序文件 WDK
- 商用测试证书 WDK
- 企业 CA 测试证书 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34cbf360689a8c845a856dab98a300d6644e1662
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377245"
---
# <a name="test-signing-a-driver-file"></a>对驱动程序文件进行测试签名


使用[ **SignTool** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)驱动程序文件中嵌入签名，如以下主题中所述：

[使用 MakeCert 测试证书或商业测试证书在驱动程序文件中嵌入测试签名](#using-a-makecert-test-certificate-or-a-commercial-test-certificate-to-)

[使用企业 CA 测试证书在驱动程序文件中嵌入测试签名](#using-an-enterprise-ca-test-certificate-to-embed-a-test-signature-in-a)

### <a href="" id="using-a-makecert-test-certificate-or-a-commercial-test-certificate-to-"></a> 使用 MakeCert 测试证书或商业测试证书在驱动程序文件中嵌入测试签名

使用以下 SignTool 命令通过使用在驱动程序文件中嵌入签名[MakeCert 测试证书](makecert-test-certificate.md)或[商业测试证书](commercial-test-certificate.md)。

```cpp
SignTool sign /v /s TestCertStoreName /n TestCertName /t http://timestamp.verisign.com/scripts/timstamp.dll DriverFileName.sys
```

其中：

-   登录命令配置 SignTool 将驱动程序文件 DriverFileName.sys 中嵌入签名。

-   **/V**详细选项配置 SignTool 打印执行消息和警告消息。

-   **/S** *TestCertStoreName*选项提供包含名为的测试证书的测试证书存储区的名称*TestCertName*。

-   **/N** *TestCertName*选项提供名为的证书存储中安装的测试证书的名称*TestCertStoreName*。 MakeCert 测试证书或商业测试证书，可以是测试证书。

-   **/T**  *http://timestamp.verisign.com/scripts/timstamp.dll* 选项提供 VeriSign 提供的公开可用的时间戳服务器的 URL。

-   *DriverFileName.sys*是驱动程序文件的名称。

下面的命令演示如何使用 SignTool 对测试签名的驱动程序文件。 此示例将嵌入到中的签名*Toaster.sys*，后者位于*amd64*在其中运行命令的目录下的子目录。 测试证书命名为"contoso.com(test)"，它将安装在名为"PrivateCertStore。"的证书存储区

```cpp
SignTool sign /v /s PrivateCertStore /n contoso.com(test) /t http://timestamp.verisign.com/scripts/timstamp.dll amd64\toaster.sys
```

### <a href="" id="using-an-enterprise-ca-test-certificate-to-embed-a-test-signature-in-a"></a>**使用企业 CA 测试证书在驱动程序文件中嵌入测试签名**

以下 SignTool 命令假定，企业 CA 颁发测试登录到在你使用的测试证书[驱动程序包](driver-packages.md)。 如果[企业 CA 测试证书](enterprise-ca-test-certificate.md)是唯一的测试证书位于你的证书存储，可以使用以下命令仅指定其中 **/a**选项以及的名称驱动程序文件。 在这种情况下，SignTool 将找到并默认情况下使用企业 CA 的测试证书。

如果已创建或获取除了企业 CA 测试证书的其他测试证书，则必须使用 SignTool 选项 **/s**并 **/n**指定测试证书存储区的名称和安装测试证书存储区中的测试证书的名称。

```cpp
SignTool sign /v /a /t http://timestamp.verisign.com/scripts/timstamp.dll DriverFileName.sys
```

 

 





