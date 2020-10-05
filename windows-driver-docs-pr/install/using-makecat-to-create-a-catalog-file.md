---
title: 使用 MakeCat 创建目录文件
description: 使用 MakeCat 创建目录文件
ms.assetid: c9f9360b-2b1d-4060-af4d-8d281319e181
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d4b70d0c3e471b79304e0d04caaa897146a8c5b
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732717"
---
# <a name="using-makecat-to-create-a-catalog-file"></a>使用 MakeCat 创建目录文件


可以使用[MakeCat](/windows/win32/seccrypto/makecat)工具为[驱动程序包](driver-packages.md)创建[编录文件](catalog-files.md)。

只有使用 MakeCat 工具才能为未使用 INF 文件安装的驱动程序包创建编录文件。 如果使用 INF 文件安装了驱动程序包，请使用 [**Inf2Cat**](../devtest/inf2cat.md) 工具创建编录文件。 Inf2Cat 自动包括在包的 INF 文件中引用的驱动程序包中的所有文件。 有关如何使用 Inf2Cat 工具的详细信息，请参阅 [使用 Inf2Cat 创建编录文件](using-inf2cat-to-create-a-catalog-file.md)。

**注意**   你还可以将签名嵌入[驱动程序包](driver-packages.md)的内核模式二进制文件（如驱动程序和包可能提供的任何 .dll 文件），而不是创建和签名目录文件。 有关此过程的详细信息，请参阅 [通过嵌入签名对驱动程序进行测试签名](test-signing-a-driver-through-an-embedded-signature.md)。

 

若要创建目录文件，必须首先手动创建目录定义文件 (*cdf*) ，其中描述了目录标头属性和文件项。 创建该文件后，你可以运行 [MakeCat](/windows/win32/seccrypto/makecat) 工具来创建编录文件。 MakeCat 工具在处理 *cdf* 文件时执行以下操作：

-   验证在 *cdf* 文件中列出的每个文件的属性列表。

-   将列出的属性添加到 [目录文件](catalog-files.md)中。

-   为列出的每个文件生成加密哈希或 *指纹*。

-   将每个文件的指纹存储在目录文件中。

本主题介绍如何为*toastpkg.inf*示例驱动程序包的64位内核模式二进制文件创建一个文件 *。* 在 WDK 安装目录中，这些二进制文件位于 *src \\ general \\ toaster \\ toastpkg.inf \\ toastcd \\ amd64* 目录中。

若要为*toastpkg.inf*示例[驱动程序包](driver-packages.md)创建一个*cdf*文件，请执行以下操作：

1.  启动记事本并复制以下示例中的文本。 它包含要分类的文件的列表及其属性。

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

2.  将该文件另存为与驱动程序包相同的文件夹中的*tstamd64。*
    **注意**   为多个平台构建驱动程序时，为每个平台创建一个单独的目录文件。

     

以下命令行说明了如何通过 [MakeCat](/windows/win32/seccrypto/makecat) 工具使用 *tstamd64* 文件创建目录文件：

```cpp
makecat -v tstamd64.cdf
```

运行该工具后，将创建一个名为 *tstamd64.cat* 的文件。

有关 MakeCat 工具及其命令行参数的详细信息，请参阅 [使用 MakeCat](/windows/win32/seccrypto/using-makecat) 网站。

有关如何使用 MakeCat 工具的详细信息，请参阅 [为非 PnP 驱动程序包创建编录文件](creating-a-catalog-file-for-a-non-pnp-driver-package.md)。

