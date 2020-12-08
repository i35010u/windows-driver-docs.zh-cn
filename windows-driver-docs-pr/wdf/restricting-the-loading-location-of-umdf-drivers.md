---
title: 限制 UMDF 驱动程序的加载位置
description: 限制 UMDF 驱动程序的加载位置
keywords:
- 位置 WDK UMDF
- 二进制文件 WDK UMDF
- 目录 WDK UMDF
- UMDriverCopy
- 正在加载位置 WDK UMDF
- INF 文件 WDK UMDF，加载位置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0f341fc428a1dfa9a4a2a9443936280ae3089ec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825283"
---
# <a name="restricting-the-loading-location-of-umdf-drivers"></a>限制 UMDF 驱动程序的加载位置


UMDF 平台将无法从% SystemRoot% \\ System32 \\ 驱动程序 UMDF 目录以外的任何位置加载主 UMDF 驱动程序二进制文件 \\ 。 因此，UMDF INF 文件必须限制将 UMDF 驱动程序安装到该目录的位置。 在此目录中安装还可确保无特权用户无法篡改 UMDF 驱动程序。

若要将 UMDF 驱动程序二进制文件安装到% SystemRoot% \\ System32 \\ 驱动程序 \\ UMDF，UMDF 驱动程序 inf 文件必须包含一个 [**INF DestinationDirs 节**](../install/inf-destinationdirs-section.md) ，该部分类似于以下代码示例。

```cpp
[DestinationDirs]
UMDriverCopy=12,UMDF ; copies to drivers\umdf
```

"UMDriverCopy" 代表一个由 INF 编写者确定的部分名称，其中列出了 UMDF 驱动程序二进制文件，如下面的示例中所示。

```cpp
[UMDriverCopy]
WUDFOsrUsbDriver.dll
```

[**CopyFiles 指令**](../install/inf-copyfiles-directive.md)还必须引用 **UMDriverCopy** 部分，以指示操作系统要从源媒体复制到目标的 UMDF 驱动程序二进制文件列表，如下面的示例中所示。

```cpp
[OsrUsb_Install.NT]
CopyFiles=UMDriverCopy
```

 

