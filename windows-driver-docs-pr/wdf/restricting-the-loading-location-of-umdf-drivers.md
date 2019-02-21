---
title: 限制 UMDF 驱动程序的加载位置
description: 限制 UMDF 驱动程序的加载位置
ms.assetid: eac19fa8-2889-4cc3-9f4b-d11d7d3ed684
keywords:
- 位置 WDK UMDF
- WDK UMDF 的二进制文件
- 目录 WDK UMDF
- UMDriverCopy
- 正在加载位置 WDK UMDF
- INF 文件 WDK UMDF，正在加载位置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4232d013b5cd416928241301aa7d1d4386f06aaa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521890"
---
# <a name="restricting-the-loading-location-of-umdf-drivers"></a>限制 UMDF 驱动程序的加载位置


UMDF 平台将无法从 %systemroot%之外的任何位置加载主 UMDF 驱动程序二进制文件\\System32\\驱动程序\\Umdf 目录。 因此，UMDF INF 文件必须限制其中 UMDF 驱动程序安装到该目录的位置。 在此目录中安装还可确保非特权的用户无法篡改 UMDF 驱动程序。

若要将 UMDF 驱动程序二进制文件安装到 %systemroot%\\System32\\驱动程序\\Umdf，UMDF 驱动程序 INF 文件必须包含[ **INF DestinationDirs 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547383)这是类似于下面的代码示例。

```cpp
[DestinationDirs]
UMDriverCopy=12,UMDF ; copies to drivers\umdf
```

"UMDriverCopy"表示确定 INF 编写器的名称的一个部分，其中列出了 UMDF 驱动程序二进制文件，在下面的示例所示。

```cpp
[UMDriverCopy]
WUDFOsrUsbDriver.dll
```

[ **CopyFiles 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546346)还必须引用**UMDriverCopy**部分，以便指出要将源中复制的操作系统的 UMDF 驱动程序二进制文件的列表目标位置，如以下示例所示的媒体。

```cpp
[OsrUsb_Install.NT]
CopyFiles=UMDriverCopy
```

 

 





