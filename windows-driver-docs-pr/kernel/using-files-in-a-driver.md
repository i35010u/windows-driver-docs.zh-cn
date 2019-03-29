---
title: 在驱动程序中使用文件
description: 在驱动程序中使用文件
ms.assetid: 721bf336-1d1d-4677-843d-8af04c6f434d
keywords:
- 文件 WDK 内核
- 文件对象 WDK 内核
- WDK 文件对象的对象
- 文件句柄 WDK 内核
- 文件 WDK 内核的句柄
- 从文件读取数据
- 向文件写入数据
- 读取文件的元数据
- 写入文件的元数据
- 驱动程序文件对象 WDK 内核
- 多个文件对象 WDK 内核
- 内核模式驱动程序 WDK，文件
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89ab1455fd941dce3461e0dea4f8d0ee2ffd5ee0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566164"
---
# <a name="using-files-in-a-driver"></a>在驱动程序中使用文件





Microsoft Windows 高级管理人员表示按文件*的文件对象*，这是由对象管理器管理的管理层对象。 （目录也表示文件对象。）

内核模式组件引用的文件按其对象名称，即 **\\DosDevices**串联到文件的完整路径。 (在 Microsoft Windows 2000 和更高版本的操作系统，  **\\??** 等效于 **\\DosDevices**。)例如，在 c： 驱动器的对象名称\\WINDOWS\\example.txt 文件 **\\DosDevices\\c:\\WINDOWS\\example.txt**。 使用对象名称以打开文件的句柄。 有关对象名称的详细信息，请参阅[对象名称](object-names.md)。

### <a name="to-use-a-file"></a>若要使用的文件

1.  打开文件的句柄。

    有关详细信息，请参阅[打开文件的句柄](opening-a-handle-to-a-file.md)。

2.  执行预期的操作通过调用适当**Zw*Xxx*文件**例程。

    有关详细信息，请参阅[使用文件句柄](using-a-file-handle.md)。

3.  通过调用关闭句柄[ **ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)。

每次打开文件的句柄的 Windows 管理人员所创建的文件对象来表示该文件，并对该对象返回打开的句柄。 因此，单个文件可以存在多个文件对象。 （在用户模式应用程序可以复制句柄，因为多个句柄也可存在相同的文件对象。）关闭所有打开的句柄的文件对象后，Windows 高级管理人员将删除的文件对象。

 

 




