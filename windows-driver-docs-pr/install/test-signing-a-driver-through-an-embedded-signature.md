---
title: 通过嵌入式签名对驱动程序进行测试签名
description: 通过嵌入式签名对驱动程序进行测试签名
ms.assetid: 862e89e0-f84a-4058-a32f-09ae3043b884
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51b7363da1b99d3521e44bfe86d010d741b7f0d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380969"
---
# <a name="test-signing-a-driver-through-an-embedded-signature"></a>通过嵌入式签名对驱动程序进行测试签名


有符号[编录文件](catalog-files.md)是所有这些必须具有正确安装并加载大多数[驱动程序包](driver-packages.md)。 但是，嵌入签名也可能是一个选项。 嵌入签名是指将数字签名添加到驱动程序的二进制图像文件本身，而不是在编录文件中保存的数字签名。 因此，嵌入签名驱动程序时修改驱动程序的二进制图像。

嵌入签名的内核模式二进制文件 （例如，驱动程序和关联的.dll 文件） 所需时：

-   该驱动程序是一个引导启动驱动程序。 在 64 位版本的 Windows Vista 和更高版本的 Windows 中，内核模式代码签名要求必须具有嵌入式的签名。 这是必需而不考虑是否驱动程序的驱动程序包已进行数字签名的目录文件。

-   通过不包括目录文件的驱动程序包安装该驱动程序。

如同[编录文件](catalog-files.md)， [ **SignTool** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)用于通过使用测试证书嵌入在内核模式二进制文件中的数字签名。 下面的命令行显示了如何运行 SignTool 将执行以下操作：

-   测试签名 Toastpkg 示例的 64 位版本的二进制文件、 toaster.sys。 在 WDK 安装目录中，此文件位于*src\\常规\\toaster\\toastpkg\\toastcd\\amd64*目录。

-   将从 PrivateCertStore Contoso.com(Test) 证书用于测试签名。 有关如何创建此证书的详细信息，请参阅[创建测试证书](creating-test-certificates.md)。

-   时间戳的时间戳颁发机构 (TSA) 通过数字签名。

对测试签名*toaster.sys*文件，请运行以下命令行：

```cpp
Signtool sign /v /fd sha256 /s PrivateCertStore /n Contoso.com(Test) /t http://timestamp.verisign.com/scripts/timestamp.dll amd64\toaster.sys
```

其中：

-   **登录**命令配置指定的目录文件进行签名的 SignTool tstamd64.cat。

-   **/V**选项启用详细的操作，在其中 SignTool 显示成功执行消息和警告消息。

-   **/Fd**选项指定要用于创建文件签名的文件摘要算法。 默认值为 SHA1。

-   **/S**选项指定的证书存储区的名称 (*PrivateCertStore)* 包含的测试证书。

-   **/N**选项指定的证书名称 (*Contoso.com(Test))* 安装指定的证书存储区中。

-   **/T**选项指定 TSA 的 URL ( *http://timestamp.verisign.com/scripts/timestamp.dll* ) 这将时间戳的数字签名。
    **重要**  泄露密钥吊销签名者的代码签名的私钥的情况下包括时间戳提供所需的信息。

     

-   *amd64\\toaster.sys*指定将嵌入已签名的内核模式二进制文件的名称。

有关 SignTool 及其命令行参数的详细信息，请参阅[ **SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)。

有关如何对测试签名的驱动程序使用嵌入式的签名的详细信息，请参阅[测试签名的驱动程序文件](test-signing-a-driver-file.md)。

 

 





