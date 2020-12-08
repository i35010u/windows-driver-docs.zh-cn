---
title: 通过嵌入式签名对驱动程序进行发布签名
description: 通过嵌入式签名对驱动程序进行发布签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2a2f848215985113dce7c59cf20f130b2123793
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839071"
---
# <a name="release-signing-a-driver-through-an-embedded-signature"></a>通过嵌入式签名对驱动程序进行发布签名

已签名的 [目录文件](catalog-files.md) 是指正确安装和加载大多数 [驱动程序包](driver-packages.md)所必需的。 不过，也可以选择嵌入签名。 嵌入签名指的是将数字签名添加到驱动程序的二进制图像文件本身，而不是在目录文件中保存数字签名。 因此，在嵌入驱动程序时，将修改驱动程序的二进制图像。

在以下情况下，需要对内核模式二进制文件的嵌入签名 (例如，驱动程序和关联的 .dll 文件) ：

- 该驱动程序是 *启动启动驱动程序*。 在 Windows Vista 和更高版本的 windows 的64位版本中， [内核模式代码签名要求](kernel-mode-code-signing-requirements--windows-vista-and-later-.md) 表明 *启动启动驱动程序* 必须具有嵌入签名。 无论驱动程序的驱动程序包是否有经过数字签名的目录文件，此项都是必需的。

- 驱动程序通过不包含目录文件的驱动程序包进行安装。

与 [目录文件](catalog-files.md)一样， [**SignTool**](../devtest/signtool.md) 工具用于通过使用测试证书嵌入内核模式二进制文件中的数字签名。 以下命令行说明了如何运行 SignTool 来执行以下操作：

- 对64位版本的 Toastpkg.inf 示例二进制文件进行测试签名，toaster.sys。 在 WDK 安装目录中，此文件位于 *src \\ general \\ toaster \\ toastpkg.inf \\ toastcd \\ amd64* 目录中。

- 使用商业证书颁发机构 (CA) 颁发的 [软件发行者证书 (SPC) ](software-publisher-certificate.md) 。

- 为 SPC 使用兼容的交叉证书。

- 通过时间戳颁发机构 (TSA) 为数字签名分配时间戳。

若要对 *toaster.sys* 文件进行测试签名，请运行以下命令行：

```cpp
Signtool sign /v /fd sha256 /ac MSCV-VSClass3.cer /s MyPersonalStore /n contoso.com /t http://timestamp.digicert.com amd64\toaster.sys
```

其中：

- **Sign** 命令将 SignTool 配置为对指定的内核模式二进制文件（ *amd64 \\toaster.sys*）进行签名。

- **/V** 选项启用详细操作，其中，SignTool 显示成功执行和警告消息。

- **/Fd** 选项指定用于创建文件签名的文件摘要算法。 默认值为 SHA1。

- **/Ac** 选项指定文件的名称，该文件包含从 CA 获取的交叉证书 (*MSCV-VSClass3*) 。 如果交叉证书不在当前目录中，请使用完整路径名称。

- **/S** 选项指定包含 SPC (*MyPersonalStore)* 的个人证书存储的名称。

- **/N** 选项指定在指定的证书存储中安装的证书 (*Contoso.com)* 的名称。

- **/T** 选项指定 `http://timestamp.digicert.com` 将对数字签名进行时间戳的 TSA () 的 URL。

>[!IMPORTANT]
>包含时间戳会提供密钥吊销所需的信息，以防签名者的代码签名私钥泄漏。

- *amd64 \\toaster.sys* 指定将被嵌入签名的内核模式二进制文件的名称。

有关 SignTool 及其命令行参数的详细信息，请参阅 [**SignTool**](../devtest/signtool.md)。

有关通过嵌入签名对驱动程序进行发布签名的详细信息，请参阅 [发布签名驱动程序包](release-signing-driver-packages.md) 和 [对驱动程序文件进行发布签名](release-signing-a-driver-file.md)。
