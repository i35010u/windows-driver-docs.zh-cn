---
title: 使用 MakeCat 创建目录文件
description: 使用 MakeCat 创建目录文件
ms.assetid: c9f9360b-2b1d-4060-af4d-8d281319e181
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e7d12ed9e28314a71e4496a2375935f9d43da99
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384758"
---
# <a name="using-makecat-to-create-a-catalog-file"></a>使用 MakeCat 创建目录文件


可以使用[MakeCat](https://go.microsoft.com/fwlink/p/?linkid=104922)工具来创建[编录文件](catalog-files.md)有关[驱动程序包](driver-packages.md)。

必须使用 MakeCat 工具只是为了创建目录文件的情况下使用 INF 文件不安装的驱动程序包。 如果要安装驱动程序包，请使用 INF 文件，使用[ **Inf2Cat** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/inf2cat)工具创建目录文件。 Inf2Cat 自动包含在包的 INF 文件中引用的驱动程序包中的所有文件。 有关如何使用 Inf2Cat 工具的详细信息，请参阅[使用 Inf2Cat 创建编录文件](using-inf2cat-to-create-a-catalog-file.md)。

**请注意**  而不是创建和签名目录文件，则也可以嵌入一个签名的内核模式二进制文件中您[驱动程序包](driver-packages.md)，如驱动程序和包可能会提供任何.dll 文件。 有关此过程的详细信息，请参阅[测试签名的驱动程序通过嵌入式签名](test-signing-a-driver-through-an-embedded-signature.md)。

 

若要创建一个目录文件，您必须首先手动创建目录定义文件 ( *.cdf*)，用于说明目录标头属性和文件条目。 此文件创建后，可以运行[MakeCat](https://go.microsoft.com/fwlink/p/?linkid=104922)工具创建目录文件。 MakeCat 工具处理时将执行以下 *.cdf*文件：

-   验证的每个文件中列出的属性列表 *.cdf*文件。

-   将添加到列出的属性[编录文件](catalog-files.md)。

-   生成加密哈希，或*指纹*，每个列出的文件。

-   目录文件中存储的每个文件的指纹。

本主题介绍如何创建 *.cdf* 64 位内核模式二进制文件的文件*ToastPkg*示例驱动程序包。 在 WDK 安装目录中，这些二进制文件都位于*src\\常规\\toaster\\toastpkg\\toastcd\\amd64*目录。

若要创建 *.cdf*适用于文件*ToastPkg*示例[驱动程序包](driver-packages.md)，执行以下操作：

1.  启动记事本并复制以下示例中的文本。 它包含要被编录，以及其属性的文件列表。

    ```cpp
    [CatalogHeader]
    Name=tstamd64.cat
    PublicVersion=0x0000001
    EncodingType=0x00010001
    CATATTR1=0x10010001:OSAttr:2:6.0
    [CatalogFiles]
    <hash>File1=amd64\toaster.pdb
    <hash>File2=amd64\toaster.sys
    <hash>File3=amd64\toastva.exe
    <hash>File4=amd64\toastva.pdb
    <hash>File5=amd64\tostrcls.dll
    <hash>File6=amd64\tostrcls.pdb
    <hash>File7=amd64\tostrco2.dll
    <hash>File8=amd64\tostrco2.pdb
    ```

2.  将该文件作为*tstamd64.cdf*驱动程序包所在的文件夹中。
    **请注意**  时生成的多个平台的驱动程序，创建每个平台的单独目录文件。

     

下面的命令行演示如何创建编录文件通过[MakeCat](https://go.microsoft.com/fwlink/p/?linkid=104922)使用的工具*tstamd64.cdf*文件：

```cpp
makecat -v tstamd64.cdf
```

在运行该工具，名为的文件后*tstamd64.cat*创建。

有关 MakeCat 工具和其命令行自变量的详细信息，请参阅[使用 MakeCat](https://go.microsoft.com/fwlink/p/?linkid=70086)网站。

有关如何使用 MakeCat 工具的详细信息，请参阅[为非 PnP 驱动程序包创建编录文件](creating-a-catalog-file-for-a-non-pnp-driver-package.md)。

 

 





