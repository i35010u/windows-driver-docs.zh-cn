---
title: 安装 PCL XL 微型驱动程序
description: 安装 PCL XL 微型驱动程序
keywords:
- PCL XL vector graphics WDK Unidrv，安装微型驱动程序
- 微型驱动程序 WDK PCL XL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d93dc46132d5383496ff8fb84686ef592518de2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796727"
---
# <a name="installing-a-pcl-xl-minidriver"></a>安装 PCL XL 微型驱动程序





在 Windows XP 和更高版本中，ntprint.inf 具有以下 \[ PCLXL。OEM \] 部分：

```cpp
[PCLXL.OEM]
CopyFiles=PCLXL,@PCL5ERES.DLL
```

[**INF CopyFiles 指令**](../install/inf-copyfiles-directive.md)将 PCLXL 节中列出的所有文件以及 \[ \] pcl5eres.dll 复制到默认目标目录。 \[PCLXL \] 节还显示在 ntprint.inf 中，并列出要复制的文件。

```cpp
[PCLXL]
PCLXL.DLL
PCLXL.GPD
P6FONT.GPD
PJL.GPD
P6DISP.GPD
```

Pclxl.dll 包含 PCL XL *UFMs* 和各种资源字符串。 本节中列出的其他 GPDs 为 PCL XL (PCL-6) 支持文件。

若要安装 PCL XL printer 微型驱动程序，OEM 应在打印机特定的 INF 中添加类似于以下内容的部分。 此 INF 在 ntprint.inf 之前加载。

```cpp
[P6SAMPLE.GPD]
CopyFiles=@P6SAMPLE.GPD
DataSection=UNIDRV_DATA
DataFile=P6SAMPLE.GPD
Include=NTPRINT.INF
Needs=UNIDRV.OEM,TTFSUB.OEM,PCLXL.OEM
```

在前面的部分中，第一行中的 **CopyFiles** 指令将) 此示例中名为 P6SAMPLE 的 OEM 的 GPD 文件复制 (。 与第二行中的 **DataSection** 指令关联的条目 (参阅 " [打印机 inf 文件数据" 部分](printer-inf-file-data-sections.md) 和 " [打印机 inf 文件安装" 部分](printer-inf-file-install-sections.md)) 引用 ntprint.inf 中的 " \[ UNIDRV Data" \_ \] 部分。 第三行中 **的数据文件指令指定** p6sample 是与此 printer 微型驱动程序关联的数据文件。 第四行使 ntprint.inf 包含在内。 第五行的 **需求** 指令中的三个条目引用了 ntprint.inf 中同名的部分。 这会使 INF 文件能够访问 driver.cab 中加载的文件。

有关使用 **CopyFiles** 指令进行打印机安装的其他信息，请参阅 [Printer INF File CopyFiles 部分](printer-inf-file-copyfiles-sections.md)。

 

