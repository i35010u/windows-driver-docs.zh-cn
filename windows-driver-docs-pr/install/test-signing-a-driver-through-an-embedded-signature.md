---
title: 通过嵌入式签名对驱动程序进行测试签名
description: 通过嵌入式签名对驱动程序进行测试签名
ms.assetid: 862e89e0-f84a-4058-a32f-09ae3043b884
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d87e9efdc235cbaed6c4a8ecf200811c6ff7ca20
ms.sourcegitcommit: a44ade167cdfb541cf1818e9f9e3726f23f90b66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361383"
---
# <a name="test-signing-a-driver-through-an-embedded-signature"></a>通过嵌入式签名对驱动程序进行测试签名

已签名的 [目录文件](catalog-files.md) 是指正确安装和加载大多数 [驱动程序包](driver-packages.md)所必需的。 不过，也可以选择嵌入签名。 嵌入签名指的是将数字签名添加到驱动程序的二进制图像文件本身，而不是在目录文件中保存数字签名。 因此，在嵌入驱动程序时，将修改驱动程序的二进制图像。

在以下情况下，需要对内核模式二进制文件的嵌入签名 (例如，驱动程序和关联的 .dll 文件) ：

-   该驱动程序是启动启动驱动程序。 在 Windows Vista 和更高版本的 windows 的64位版本中，内核模式代码签名要求表明 *启动启动驱动程序* 必须具有嵌入签名。 无论驱动程序的驱动程序包是否有经过数字签名的目录文件，此项都是必需的。

- 驱动程序通过不包含目录文件的驱动程序包进行安装。

对于 [目录文件](catalog-files.md)， [**SignTool**](../devtest/signtool.md) 用于通过使用测试证书嵌入内核模式二进制文件中的数字签名。 以下命令行说明了如何运行 SignTool 来执行以下操作：

- 对64位版本的 Toastpkg.inf 示例二进制文件进行测试签名，toaster.sys。 在 WDK 安装目录中，此文件位于 *src \\ general \\ toaster \\ toastpkg.inf \\ toastcd \\ amd64* 目录中。

- 使用 Contoso.com (测试 PrivateCertStore 中的) 证书来测试签名。 有关如何创建此证书的详细信息，请参阅 [创建测试证书](creating-test-certificates.md)。

- 时间戳通过时间戳颁发机构 (TSA) 进行数字签名。

若要对 *toaster.sys* 文件进行测试签名，请运行以下命令行：

```cpp
Signtool sign /v /fd sha256 /s PrivateCertStore /n Contoso.com(Test) /t http://timestamp.digicert.com amd64\toaster.sys
```

其中：

- **Sign** 命令将 SignTool 配置为对指定的编录文件 tstamd64.cat 进行签名。

- **/V** 选项启用详细操作，其中，SignTool 显示成功执行和警告消息。

- **/Fd** 选项指定用于创建文件签名的文件摘要算法。 默认值为 SHA1。

- **/S** 选项指定包含测试证书的证书存储 ( *PrivateCertStore)* 的名称。

- **/N** 选项指定在指定的证书存储中安装的 ( *Contoso.com (测试) # B3* 的证书的名称。

- **/T** 选项指定了 `http://timestamp.digicert.com` 用于对数字签名进行时间戳的 TSA () 的 URL。

>[!IMPORTANT]
>包含时间戳会提供密钥吊销所需的信息，以防签名者的代码签名私钥泄漏。

- *amd64 \\toaster.sys* 指定将被嵌入签名的内核模式二进制文件的名称。

有关 SignTool 及其命令行参数的详细信息，请参阅 [**SignTool**](../devtest/signtool.md)。

有关如何使用嵌入的签名对驱动程序进行测试签名的详细信息，请参阅对 [驱动程序文件进行测试签名](test-signing-a-driver-file.md)。