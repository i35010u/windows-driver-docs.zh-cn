---
title: 通过嵌入式签名对驱动程序进行测试签名
description: 通过嵌入式签名对驱动程序进行测试签名
ms.assetid: 862e89e0-f84a-4058-a32f-09ae3043b884
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcbd3e281cfce1f8bec6741c21cb0fe7097c4e52
ms.sourcegitcommit: 238308264c1ee2c74ec0c8c303258dc00c79b902
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2019
ms.locfileid: "70063927"
---
# <a name="test-signing-a-driver-through-an-embedded-signature"></a>通过嵌入式签名对驱动程序进行测试签名


已签名的[目录文件](catalog-files.md)是指正确安装和加载大多数[驱动程序包](driver-packages.md)所必需的。 不过, 也可以选择嵌入签名。 嵌入签名指的是将数字签名添加到驱动程序的二进制图像文件本身, 而不是在目录文件中保存数字签名。 因此, 在嵌入驱动程序时, 将修改驱动程序的二进制图像。

在以下情况下, 需要对内核模式二进制文件 (例如, 驱动程序和关联的 .dll 文件) 进行嵌入签名:

-   该驱动程序是启动启动驱动程序。 在 Windows Vista 和更高版本的 windows 的64位版本中, 内核模式代码签名要求必须具有嵌入签名。 无论驱动程序的驱动程序包是否有经过数字签名的目录文件, 此项都是必需的。

-   驱动程序通过不包含目录文件的驱动程序包进行安装。

对于[目录文件](catalog-files.md), [**SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)用于通过使用测试证书嵌入内核模式二进制文件中的数字签名。 以下命令行说明了如何运行 SignTool 来执行以下操作:

-   对64位版本的 Toastpkg.inf 示例的二进制文件 toaster 进行测试签名。 在 WDK 安装目录中, 此文件位于*src\\general\\toaster\\\\toastpkg.inf\\toastcd amd64*目录中。

-   使用 PrivateCertStore 中的 Contoso .com (Test) 证书作为测试签名。 有关如何创建此证书的详细信息, 请参阅[创建测试证书](creating-test-certificates.md)。

-   时间戳通过时间戳颁发机构 (TSA) 进行数字签名的时间戳。

若要对*toaster*文件进行测试签名, 请运行以下命令行:

```cpp
Signtool sign /v /fd sha256 /s PrivateCertStore /n Contoso.com(Test) /t http://timestamp.digicert.com amd64\toaster.sys
```

其中：

-   **Sign**命令将 SignTool 配置为对指定的编录文件 tstamd64.cat 进行签名。

-   **/V**选项启用详细操作, 其中, SignTool 显示成功执行和警告消息。

-   **/Fd**选项指定用于创建文件签名的文件摘要算法。 默认值为 SHA1。

-   **/S**选项指定包含测试证书的证书存储 (*PrivateCertStore)* 的名称。

-   **/N**选项指定在指定的证书存储中安装的证书 (*Contoso .com (Test))* 的名称。

-   **/T**选项指定将对数字签名进行时间 *http://timestamp.digicert.com* 戳的 TSA () 的 URL。
    **重要提示**  如果签名者的代码签名私钥被泄露, 则包括时间戳提供必要的密钥吊销信息。

     

-   *amd64\\toaster*指定将被嵌入签名的内核模式二进制文件的名称。

有关 SignTool 及其命令行参数的详细信息, 请参阅[**SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)。

有关如何使用嵌入的签名对驱动程序进行测试签名的详细信息, 请参阅对[驱动程序文件进行测试签名](test-signing-a-driver-file.md)。

 

 





