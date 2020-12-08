---
title: 验证发布签名
description: 验证发布签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 580e71d3e83efa0479d558297ac94a9a43f281be
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840947"
---
# <a name="verifying-the-release-signature"></a>验证发布签名


[驱动程序包](driver-packages.md)经过版本签名后，可以使用 [**SignTool**](../devtest/signtool.md)工具来验证的签名：

-   驱动程序包中的单个文件。

-   已嵌入签名的内核模式二进制文件（如驱动程序）。

本主题中的示例使用 Toastpkg.inf 示例二进制文件的64位版本 *toaster.sys*。 在 WDK 安装目录中，此文件位于 *src \\ general \\ toaster \\ toastpkg.inf \\ toastcd \\ amd64* 目录中。

下面的示例在 *tstamd64.cat* release 签名 [目录文件](catalog-files.md)中验证 *toaster.sys* 的签名：

```cpp
Signtool verify /kp /v /c tstamd64.cat amd64\toaster.sys
```

其中：

-   **Verify** 命令将 SignTool 配置为验证指定 [目录文件](catalog-files.md)中的签名 (*tstamd64.cat*) 。

-   **/Kp** 选项将 SignTool 配置为验证是否已满足内核策略。

-   **/V** 选项将 SignTool 配置为打印执行和警告消息。

-   **/C** 选项指定已发布签名 (*tstamd64.cat*) 的驱动程序包的 [目录文件](catalog-files.md)。 如果要验证嵌入签名的驱动程序的数字签名，请不要使用此选项。

-   *amd64 \\toaster.sys* 是要验证的文件的名称。

在标记为 "签名证书链" 的此命令的输出下，应验证是否满足以下条件：

-   内核策略的证书链的根由 Microsoft 代码验证根颁发给和。

-   颁发给类3公共主证书颁发机构的交叉证书也由 Microsoft 代码验证根颁发。

对于签名的目录文件，还可以在驱动程序包内的任何内核模式二进制文件中验证默认的 Authenticode 验证策略签名。 这可确保该文件在用户模式即插即用安装对话框和 MMC 设备管理器管理单元中显示为已签名。

**注意**  此示例仅用于验证已发布签名的 [目录文件](catalog-files.md) ，而不是嵌入签名的内核模式二进制文件。

 

以下示例在 *tstamd64.cat* 签名目录文件中验证 *toaster.sys* 的默认 Authenticode 验证策略：

```cpp
Signtool verify /pa /v /c tstamd64.cat amd64\toaster.sys
```

其中：

- **Verify** 命令将 SignTool 配置为验证指定文件中的签名 <em>。</em>

- **/Pa** 选项将 SignTool 配置为验证是否已满足验证码验证策略。

- **/V** 选项将 SignTool 配置为打印执行和警告消息。

- **/C** 选项指定已发布签名 (*tstamd64.cat*) 的驱动程序包的 [目录文件](catalog-files.md)。

- *amd64 \\toaster.sys* 是要验证的文件的名称。

在标记为 "签名证书链" 的此命令的输出下，你应验证是否向颁发了默认的 Authenticode 证书链，并由第3类公共主证书颁发机构颁发。

还可以通过执行以下步骤，通过 Windows 资源管理器验证目录文件本身的数字签名：

-   右键单击该 [目录文件](catalog-files.md) ，然后选择 " **属性**"。

-   对于经过数字签名的文件，该文件的 " **属性** " 对话框将显示 "其他 **数字签名** " 选项卡，在该选项卡上会显示用于对文件进行签名的证书的签名、时间戳和详细信息。

有关如何发布驱动程序包的详细信息，请参阅 [发布签名驱动程序包](release-signing-driver-packages.md) 和 [验证编录文件的 SPC 签名](verifying-the-spc-signature-of-a-catalog-file.md)。

 

