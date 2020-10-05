---
title: 为非 PnP 驱动程序包创建目录文件
description: 为非 PnP 驱动程序包创建目录文件
ms.assetid: b40a6f42-53a8-468f-abf1-335c5ead3cbd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e25c0d5d789076d046873cfc6d693a32daecbcf
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733179"
---
# <a name="creating-a-catalog-file-for-a-non-pnp-driver-package"></a>为非 PnP 驱动程序包创建目录文件


可以使用[MakeCat](/windows/win32/seccrypto/makecat)工具为非 PnP[驱动程序包](driver-packages.md)创建[编录文件](catalog-files.md)。

**注意**   只有使用 MakeCat 工具才能为未使用 INF 文件安装的驱动程序包创建编录文件。 如果使用 INF 文件安装了驱动程序包，请使用 [**Inf2Cat**](../devtest/inf2cat.md) 工具创建编录文件。 Inf2Cat 自动包括在包的 INF 文件中引用的驱动程序包中的所有文件。 有关如何使用 Inf2Cat 工具的详细信息，请参阅 [使用 Inf2Cat 创建编录文件](using-inf2cat-to-create-a-catalog-file.md)。

 

若要创建目录文件，必须先手动 ( 创建目录定义文件。描述目录标头属性和文件项的) *。* 创建此文件后，你可以运行 [MakeCat](/windows/win32/seccrypto/makecat) 工具来创建编录文件

### <a name="creating-a-catalog-file"></a>创建编录文件

若要为非 PnP 驱动程序包创建编录文件，请执行以下步骤：

1.  使用文本编辑器创建。*cdf* 文件，其中列出了要创建的 [目录文件](catalog-files.md) 的名称、其属性以及要在目录文件中列出的文件的名称。

2.  使用 [MakeCat](/windows/win32/seccrypto/makecat) 命令行工具创建编录文件。 有关 MakeCat 工具的详细信息，请参阅 [使用 MakeCat](/windows/win32/seccrypto/using-makecat) 网站。

3.  在将安装驱动程序的计算机上安装目录文件。

### <a name="overview-of-the-makecat-tool"></a>MakeCat 工具概述

MakeCat 工具在处理时执行以下过程。*cdf* 文件：

-   验证所定义的 [目录文件](catalog-files.md) 的特性。*cdf* 文件，并将属性添加到目录文件中。

-   验证中列出的每个文件的属性。*cdf* 文件，并将属性添加到目录文件中。

-   为列出的每个文件生成加密哈希或 *指纹*。

-   将每个文件的指纹存储在目录文件中。

使用以下 MakeCat 命令创建编录文件。

```cpp
MakeCat -v CatalogDefinitionFileName..cdf
```

其中：

-   **-V**选项将 MakeCat 配置为打印执行和警告消息。

-   *CatalogDefinitionFileNamecdf* 是目录定义文件的名称。

### <a name="examples"></a>示例

下面的示例显示名为 "良好" 的典型目录定义文件的内容。cdf. 要编录的包包含两个文件： *File1* 和 *File2*。 生成的目录文件的名称为 Good.cat。

```cpp
[CatalogHeader]
Name=Good.cat
PublicVersion=0x0000001
EncodingType=0x00010001
CATATTR1=0x10010001:OSAttr:2:6.0
[CatalogFiles]
<hash>File1=File1
<hash>File2=File2
```

下面介绍了本示例中使用的选项。 有关这些选项的详细信息，请参阅 [MakeCat](/windows/win32/seccrypto/makecat) 网站。

<a href="" id="name-good-cat"></a>名称 = 好的 .cat  
指定 (*Good.cat*) 的目录文件的名称。

<a href="" id="publicversion-0x0000001"></a>PublicVersion = 0x0000001  
指定目录文件的版本。

<a href="" id="encodingtype-0x00010001"></a>EncodingType = 0x00010001  
指定用于生成指纹的消息编码类型。 值0x00010001 指定 PKCS_7_ASN_ENCODING 的消息编码类型 |X509_ASN_ENCODING。

<a href="" id="catattr1-0x10010001-osattr-2-6-0"></a>CATATTR1 = 0x10010001： OSAttr：2：6。0  
指定目录文件的属性。 若要指定其他属性，必须使用单独的 CATATTR 选项，并为每个选项分配一个唯一的数字作为后缀。 例如，使用 CATATT1 指定一个目录文件属性，并使用 CATATT2 来指定另一个。

在此示例中，使用 CATATTR1 选项指定的属性具有以下值：

<a href="" id="0x10010001"></a>0x10010001  
将属性指定为以下内容：

-   指纹)  (已签名的0x10000000 身份验证的属性。

-   0x00010000-特性以纯文本形式表示。

-   0x00000001-Attribute 是一个名称-值对。

<a href="" id="osattr-2-6-0"></a>OSAttr：2：6。0  
OSAttr 特性指定其签名要求与 [驱动程序包](driver-packages.md)兼容的目标 Windows 版本。 特性的值指定以下内容：

-   值 *2* 指定目录文件与基于 NT Windows 操作系统的版本兼容。

-   值 *6.0* 指定目录文件与 Windows Vista 兼容。
    **注意**   如果[驱动程序包](driver-packages.md)与多个 windows 版本兼容，则必须使用单独的 CATATTR 选项来指定每个 windows 版本的 OSAttr 属性。

     

<a href="" id="-hash-file1-file1"></a>&lt;哈希 &gt; File1 = file1  
指定通过目录文件引用的文件 File1 的引用标记。 值* &lt; 哈希 &gt; * 1 将标记为文件的加密哈希或*指纹*。

<a href="" id="-hash-file1-file2"></a>&lt;哈希 &gt; File1 = File2  
指定通过目录文件引用的文件 File2 的引用标记。 值* &lt; 哈希 &gt; File2*会生成标记为文件的指纹。

下面的示例演示如何从相应的目录定义文件*Good.cat*生成[目录文件](catalog-files.md) *。cdf*。 Makecat 将 *Good.cat* 保存在 *File1* 和 *File2* 所在的同一文件夹中。

```cpp
MakeCat -v Good.cdf
```

