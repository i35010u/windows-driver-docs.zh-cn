---
title: 45 示例添加和删除驱动程序包
description: 45 示例添加和删除驱动程序包
ms.assetid: 36da02d7-0b8f-40ed-a594-0e2374595782
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8342c4db377eb4c8c0153800336349a5e514ebb6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344641"
---
# <a name="example-45-add-and-remove-driver-packages"></a>示例 45：添加和删除驱动程序包


以下示例演示如何使用 DevCon 来添加、 删除和显示在驱动程序存储区中的第三方 (OEM) 驱动程序包。

第一个命令[ **DevCon Dp\_添加**](devcon-dp-add.md)命令时，驱动程序存储区，到 WDK 中的 Toaster 示例驱动程序的副本 INF 文件，即为 %windir%\\inf 目录。 该命令包含的 Toaster 示例驱动程序的 INF 文件的完全限定的路径。

此命令适用于第三方 (OEM) 驱动程序和设备，但您可以使用 Toaster 示例来测试该命令。

```
devcon dp_add C:\WinDDK\5322\src\general\toaster\inf\i386\toaster.inf
```

在响应中，DevCon 报告它 Toaster INF 文件添加到驱动程序存储区，并将其命名为 Oem2.inf。

```
Driver Package 'oem2.inf' added.
```

然后再将它复制到驱动程序存储区，Windows 将驱动程序存储区，以确保它不添加重复的文件中的 INF 文件的二进制版本的 INF 文件的二进制版本进行比较。 例如，如果您重复该命令将 Toaster.inf 添加到驱动程序存储区，DevCon 不创建新的 OEM\*.inf 文件。 在下面的 DevCon 输出所示，它只报告现有文件的名称。

```
devcon dp_add C:\WinDDK\5322\src\general\toaste
r\inf\i386\toaster.inf
Driver Package 'oem2.inf' added.

devcon dp_add C:\WinDDK\5322\src\general\toaste
r\inf\i386\toaster.inf
Driver Package 'oem2.inf' added.
```

若要从驱动程序存储区中删除 Toaster 驱动程序的驱动程序包，必须使用 OEM\*驱动程序.inf 文件名称。 若要查找驱动程序的文件名称，请使用[ **DevCon Dp\_enum** ](devcon-dp-enum.md)命令。

以下命令列出了所有 OEM 驱动程序包和几个及其属性。

```
devcon dp_enum
```

在响应中，DevCon 生成显示在下面的：

```
c:\WinDDK\5322\tools\devcon\i386>devcon dp_enum
The following 3rd party Driver Packages are on this machine:
oem2.inf
    Provider: Microsoft
    Class: unknown
    Date: 12/10/2004
    Version: 2.0.1403.0
```

此信息指示驱动程序包由 Microsoft 提供，使用未指定的设备类 (Toaster) 名为 OEM2.inf。 此信息可用于删除与文件关联的驱动程序包。

以下命令从驱动程序存储，以及其关联的预编译的 INF (.pnf) 和目录 (.cat) 文件中删除 OEM2.inf 文件。 该命令使用 OEM\*.inf 文件的名称。

```
devcon dp_delete oem2.inf
```

在响应中，DevCon 显示一条消息，指示命令成功：

```
Driver Package 'oem2.inf' deleted.
```

OEM\*.inf 文件名中需要[ **DevCon Dp\_删除**](devcon-dp-delete.md)命令。 如果尝试使用 INF 文件的原始名称，该命令就会失败，如下面的 DevCon 输出所示。

```
devcon dp_delete C:\WinDDK\5322\src\general\toa
ster.inf
Deleting the specified Driver Package from the machine failed.
devcon failed.
```

 

 





