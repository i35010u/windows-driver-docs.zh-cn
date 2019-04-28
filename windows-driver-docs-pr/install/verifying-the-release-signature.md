---
title: 验证发布签名
description: 验证发布签名
ms.assetid: 28ed3bb6-dc57-42f9-8bd5-7118619f3bf5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc0e13a995606f97c117aacb3a3cebb6a6486a8d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339327"
---
# <a name="verifying-the-release-signature"></a>验证发布签名


之后[驱动程序包](driver-packages.md)已发布签名[ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)工具可用于验证的签名：

-   驱动程序包中的单个文件。

-   内核模式二进制文件，例如已嵌入签名的驱动程序。

本主题中的示例使用 Toastpkg 示例的二进制文件的 64 位版本*toaster.sys*。 在 WDK 安装目录中，此文件位于*src\\常规\\toaster\\toastpkg\\toastcd\\amd64*目录。

下面的示例验证的签名*toaster.sys*中*tstamd64.cat*版本签名[编录文件](catalog-files.md):

```cpp
Signtool verify /kp /v /c tstamd64.cat amd64\toaster.sys
```

其中：

-   **验证**命令将配置 SignTool 验证中指定的签名[编录文件](catalog-files.md)(*tstamd64.cat*)。

-   **/Kp**选项配置 SignTool 要验证是否已满足内核策略。

-   **/V**选项配置 SignTool 打印执行消息和警告消息。

-   **/C**选项指定驱动程序包[编录文件](catalog-files.md)的已发布签名 (*tstamd64.cat*)。 如果你要验证数字签名的嵌入签名的驱动程序，不要使用此选项。

-   *amd64\\toaster.sys*是要验证的文件的名称。

在标记为"签名证书链"此命令的输出，应验证以下条件为真：

-   与 Microsoft 代码验证根发出内核策略的证书链的根目录。

-   交叉证书中，类 3 公共主证书颁发机构颁发，也是由 Microsoft 代码验证根颁发的。

对于签名的编录文件，默认验证码验证策略可以还验证签名上驱动程序包中的任何内核模式二进制文件。 这可确保该文件将显示登录用户模式下插安装对话框和 MMC 设备管理器管理单元。

**请注意**  此示例仅用于验证的已发布签名[编录文件](catalog-files.md)和未嵌入的签名的内核模式二进制文件。

 

下面的示例验证的默认认证码验证策略*toaster.sys*中*tstamd64.cat*目录文件进行签名：

```cpp
Signtool verify /pa /v /c tstamd64.cat amd64\toaster.sys
```

其中：

- **验证**命令将配置 SignTool 将验证指定的文件中的签名<em>。</em>

- **/Pa**选项配置 SignTool 要验证是否已满足认证码验证策略。

- **/V**选项配置 SignTool 打印执行消息和警告消息。

- **/C**选项指定驱动程序包[编录文件](catalog-files.md)的已发布签名 (*tstamd64.cat*)。

- *amd64\\toaster.sys*是要验证的文件的名称。

在标记为"签名证书链"此命令的输出，应确认且可由类 3 公共主证书颁发机构颁发的默认验证码证书链。

您还可以通过执行以下步骤来验证数字签名的编录文件本身通过 Windows 资源管理器：

-   右键单击[编录文件](catalog-files.md)，然后选择**属性**。

-   为进行数字签名的文件，该文件的**属性**对话框的具有一个额外**数字签名**选项卡上，在其上的签名、 时间戳和用于对文件进行签名的证书的详细信息显示。

有关如何发布符号驱动程序包的详细信息，请参阅[版本签名驱动程序包](release-signing-driver-packages.md)并[验证目录文件的 SPC 签名](verifying-the-spc-signature-of-a-catalog-file.md)。

 

 





