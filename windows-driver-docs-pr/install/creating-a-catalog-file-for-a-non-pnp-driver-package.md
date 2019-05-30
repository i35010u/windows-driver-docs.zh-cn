---
title: 为非 PnP 驱动程序包创建目录文件
description: 为非 PnP 驱动程序包创建目录文件
ms.assetid: b40a6f42-53a8-468f-abf1-335c5ead3cbd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e301da648db48a14ae97b3635b3283a2687d350
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344335"
---
# <a name="creating-a-catalog-file-for-a-non-pnp-driver-package"></a>为非 PnP 驱动程序包创建目录文件


可以使用[MakeCat](https://go.microsoft.com/fwlink/p/?linkid=104922)工具来创建[编录文件](catalog-files.md)为非 PnP[驱动程序包](driver-packages.md)。

**请注意**  必须使用 MakeCat 工具只是为了创建目录文件的情况下使用 INF 文件不安装的驱动程序包。 如果要安装驱动程序包，请使用 INF 文件，使用[ **Inf2Cat** ](https://msdn.microsoft.com/library/windows/hardware/ff547089)工具创建目录文件。 Inf2Cat 自动包含在包的 INF 文件中引用的驱动程序包中的所有文件。 有关如何使用 Inf2Cat 工具的详细信息，请参阅[使用 Inf2Cat 创建编录文件](using-inf2cat-to-create-a-catalog-file.md)。

 

若要创建一个目录文件，您必须首先手动创建目录定义文件 (。 *。cdf*)，用于说明目录标头属性和文件条目。 创建此文件后，可以运行[MakeCat](https://go.microsoft.com/fwlink/p/?linkid=104922)工具创建目录文件

### <a name="creating-a-catalog-file"></a>创建编录文件

若要创建非 PnP 驱动程序包的目录文件，请执行以下步骤：

1.  使用文本编辑器创建。 *.cdf*列出的名称的文件[编录文件](catalog-files.md)要创建的属性，以及要在目录文件中列出的文件的名称。

2.  使用[MakeCat](https://go.microsoft.com/fwlink/p/?linkid=104922)命令行工具创建目录文件。 有关 MakeCat 工具的详细信息，请参阅[使用 MakeCat](https://go.microsoft.com/fwlink/p/?linkid=70086)网站。

3.  安装在其安装该驱动程序的计算机上的目录文件。

### <a name="overview-of-the-makecat-tool"></a>MakeCat 工具概述

MakeCat 工具执行以下处理时。 *.cdf*文件：

-   验证的特性[编录文件](catalog-files.md)由定义。 *。cdf*文件，并将属性添加到目录文件。

-   验证每个文件中列出的属性。 *.cdf*文件，并将属性添加到目录文件。

-   生成加密哈希，或*指纹*，每个列出的文件。

-   目录文件中存储每个文件的指纹。

使用以下 MakeCat 命令创建一个目录文件。

```cpp
MakeCat -v CatalogDefinitionFileName..cdf
```

其中：

-   **-V**选项配置 MakeCat 打印执行消息和警告消息。

-   *CatalogDefinitionFileName...cdf*目录定义文件的名称。

### <a name="examples"></a>示例

下面的示例显示了名为良好的典型目录定义文件的内容...cdf。 要将编入目录的包包含两个文件， *File1*并*File2*。 生成的目录文件命名为 Good.cat。

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

此示例中使用的选项如下所述。 有关这些选项的详细信息，请参阅[MakeCat](https://go.microsoft.com/fwlink/p/?linkid=104922)网站。

<a href="" id="name-good-cat"></a>Name=Good.cat  
指定的目录文件的名称 (*Good.cat*)。

<a href="" id="publicversion-0x0000001"></a>PublicVersion=0x0000001  
指定的目录文件的版本。

<a href="" id="encodingtype-0x00010001"></a>EncodingType=0x00010001  
指定消息编码类型，用于生成指纹。 值 0x00010001 指定消息编码类型的 PKCS_7_ASN_ENCODING |X509_ASN_ENCODING。

<a href="" id="catattr1-0x10010001-osattr-2-6-0"></a>CATATTR1=0x10010001:OSAttr:2:6.0  
指定目录文件的属性。 若要指定其他属性，你必须使用单独的 CATATTR 选项，每个选项分配一个唯一数字作为后缀。 例如，使用 CATATT1 指定一个目录文件属性和 CATATT2 以指定另一个。

在此示例中，使用 CATATTR1 选项指定的特性具有以下值：

<a href="" id="0x10010001"></a>0x10010001  
指定要作为以下属性：

-   0x10000000-已经过身份验证属性 （已签名，包含在指纹）。

-   0x00010000-以纯文本形式表示属性。

-   0x00000001-属性是名称 / 值对。

<a href="" id="osattr-2-6-0"></a>OSAttr:2:6.0  
OSAttr 属性指定的目标 Windows 版本的签名需求与兼容[驱动程序包](driver-packages.md)。 指定以下属性的值：

-   该值*2*指定目录文件与基于 NT 的 Windows 操作系统版本兼容。

-   该值*6.0*指定目录文件与 Windows Vista 兼容。
    **请注意**  如果[驱动程序包](driver-packages.md)是与多个 Windows 版本兼容，你必须使用单独的 CATATTR 选项来指定每个 Windows 版本的 OSAttr 属性。

     

<a href="" id="-hash-file1-file1"></a>&lt;hash&gt;File1=File1  
指定文件 File1 通过目录文件引用它的引用标记。 该值 *&lt;哈希&gt;File1*正在文件的加密哈希，该标记会导致或 *指纹*。

<a href="" id="-hash-file1-file2"></a>&lt;哈希&gt;File1 = File2  
指定的文件，文件 2，这通过目录文件引用一个引用标记。 该值 *&lt;哈希&gt;File2* 导致正在文件的指纹的标记。

下面的示例演示如何生成[编录文件](catalog-files.md)， *Good.cat，* 从相应的目录定义文件*好...cdf*。 将保存 Makecat *Good.cat*在同一文件夹中其中*File1*和*File2*所在。

```cpp
MakeCat -v Good.cdf
```

 

 





