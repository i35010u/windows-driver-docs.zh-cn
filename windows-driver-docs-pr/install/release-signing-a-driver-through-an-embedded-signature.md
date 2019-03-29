---
title: 通过嵌入式签名对驱动程序进行发布签名
description: 通过嵌入式签名对驱动程序进行发布签名
ms.assetid: ffea2479-83ee-4d94-a5e6-73ecea9fc17d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3a5211765376f79d059820454d2f7747b3256a3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569371"
---
# <a name="release-signing-a-driver-through-an-embedded-signature"></a>通过嵌入式签名对驱动程序进行发布签名


有符号[编录文件](catalog-files.md)是所有这些必须具有正确安装并加载大多数[驱动程序包](driver-packages.md)。 但是，嵌入签名也可能是一个选项。 嵌入签名是指将数字签名添加到驱动程序的二进制图像文件本身，而不是在编录文件中保存的数字签名。 因此，嵌入签名驱动程序时修改驱动程序的二进制图像。

嵌入签名的内核模式二进制文件 （例如，驱动程序和关联的.dll 文件） 所需时：

-   包含的驱动程序*引导启动驱动程序*。 在 64 位版本的 Windows Vista 和更高版本的 Windows，[内核模式代码签名要求](kernel-mode-code-signing-requirements--windows-vista-and-later-.md)指出*引导启动驱动程序*必须具有嵌入式的签名。 这是必需而不考虑是否驱动程序的驱动程序包已进行数字签名的目录文件。

-   通过不包括目录文件的驱动程序包安装该驱动程序。

如同[编录文件](catalog-files.md)，则[ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)工具用于通过使用测试证书嵌入在内核模式二进制文件中的数字签名。 下面的命令行显示了如何运行 SignTool 将执行以下操作：

-   测试签名 Toastpkg 示例的 64 位版本的二进制文件、 toaster.sys。 在 WDK 安装目录中，此文件位于*src\\常规\\toaster\\toastpkg\\toastcd\\amd64*目录。

-   使用[软件发布者证书 (SPC)](software-publisher-certificate.md)商业证书颁发机构 (CA) 颁发。

-   使用 SPC 兼容交叉证书。

-   将时间戳分配给通过时间戳颁发机构 (TSA) 的数字签名。

对测试签名*toaster.sys*文件，请运行以下命令行：

```cpp
Signtool sign /v /ac MSCV-VSClass3.cer /s MyPersonalStore /n contoso.com /t http://timestamp.verisign.com/scripts/timstamp.dll amd64\toaster.sys
```

其中：

-   **符号**命令将配置指定的内核模式二进制文件，进行签名的 SignTool *amd64\\toaster.sys*。

-   **/V**选项启用详细的操作，在其中 SignTool 显示成功执行消息和警告消息。

-   **/Ac**选项指定包含交叉证书的文件的名称 (*MSCV VSClass3.cer*) 从 CA 获取。 如果交叉证书不在当前目录中，使用的完整路径名称。

-   **/S**选项指定的个人证书存储名称 (*MyPersonalStore)* ，其中包含 SPC。

-   **/N**选项指定的证书名称 (*Contoso.com)* 安装指定的证书存储区中。

-   **/T**选项指定 TSA 的 URL (*http://timestamp.verisign.com/scripts/timstamp.dll*) 将数字签名时间戳。

    **重要**  泄露密钥吊销签名者的代码签名的私钥的情况下包括时间戳提供所需的信息。

     

-   *amd64\\toaster.sys*指定将嵌入已签名的内核模式二进制文件的名称。

有关 SignTool 及其命令行参数的详细信息，请参阅[ **SignTool**](https://msdn.microsoft.com/library/windows/hardware/ff551778)。

有关发布对通过嵌入式签名的驱动程序签名的详细信息，请参阅[版本签名驱动程序包](release-signing-driver-packages.md)并[版本签名的驱动程序文件](release-signing-a-driver-file.md)。

 

 





