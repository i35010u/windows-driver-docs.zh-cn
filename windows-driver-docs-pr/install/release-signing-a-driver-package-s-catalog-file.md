---
title: 版本签名驱动程序包的目录文件
description: 版本签名驱动程序包的目录文件
ms.assetid: 8bfedf24-403a-406e-993d-5ab8cc790f60
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a1790c394107945fd7778ec1ea377ce13453aaf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534353"
---
# <a name="release-signing-a-driver-packages-catalog-file"></a>版本签名驱动程序包的目录文件


一次[编录文件](catalog-files.md)有关[驱动程序包](driver-packages.md)创建或更新目录文件可以通过签名[ **SignTool**](https://msdn.microsoft.com/library/windows/hardware/ff551778)。 签名之后，目录文件中存储的数字签名会失效，如果驱动程序包的任何组件进行了修改。

当进行数字签名目录文件，SignTool 将保存编录文件中的数字签名。 SignTool 不更改驱动程序包的组件。 但是，由于目录文件包含的驱动程序包的组件的哈希的值，目录文件中的数字签名被维护，只要组件哈希处理为相同的值。

SignTool 还可以向数字签名添加时间戳。 时间戳就可以确定创建的签名时，并支持更灵活的证书吊销选项，如有必要。

下面的命令行显示了如何运行 SignTool 将执行以下操作：

-   发布符号*tstamd64.cat*的编录文件*ToastPkg*示例[驱动程序包](driver-packages.md)。 详细了解如何为这[编录文件](catalog-files.md)已创建，请参见[版本签名的驱动程序包创建编录文件](creating-a-catalog-file-for-release-signing-a-driver-package.md)。

-   使用[软件发布者证书 (SPC)](software-publisher-certificate.md)商业证书颁发机构 (CA) 颁发。

-   使用 SPC 兼容交叉证书。

-   将时间戳分配给通过时间戳颁发机构 (TSA) 的数字签名。

对版本签名*tstamd64.cat*目录文件，请运行以下命令行：

```cpp
Signtool sign /v /ac MSCV-VSClass3.cer /s MyPersonalStore /n contoso.com /t http://timestamp.verisign.com/scripts/timstamp.dll tstamd64.cat
```

其中：

-   **符号**命令将配置为指定的目录文件进行签名的 SignTool *tstamd64.cat*。

-   **/V**选项启用详细的操作，在其中 SignTool 显示成功执行消息和警告消息。

-   **/Ac**选项指定包含交叉证书的文件的名称 (*MSCV VSClass3.cer*) 从 CA 获取。 如果交叉证书不在当前目录中，使用的完整路径名称。

-   **/S**选项指定的个人证书存储名称 (*MyPersonalStore)* ，其中包含 SPC。

-   **/N**选项指定的 SPC 名称 (*Contoso.com)* 安装指定的证书存储区中。

-   **/T**选项指定 TSA 的 URL (*http://timestamp.verisign.com/scripts/timstamp.dll*) 将数字签名时间戳。
    **重要**  泄露密钥吊销签名者的代码签名的私钥的情况下包括时间戳提供所需的信息。

     

-   *tstamd64.cat*指定将对其进行数字签名的编录文件的名称。

有关 SignTool 及其命令行参数的详细信息，请参阅[ **SignTool**](https://msdn.microsoft.com/library/windows/hardware/ff551778)。

有关版本签名驱动程序包的详细信息，请参阅[版本签名驱动程序包](release-signing-driver-packages.md)。

 

 





