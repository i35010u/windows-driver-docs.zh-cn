---
title: 示例45添加和删除驱动程序包
description: 示例45添加和删除驱动程序包
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5761d7f94dccff28589558130ba9fff5a4eebcb5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840191"
---
# <a name="example-45-add-and-remove-driver-packages"></a>示例 45：添加和删除驱动程序包


下面的示例演示如何使用 DevCon 来添加、删除和显示驱动程序存储区中的第三方 (OEM) 驱动程序包。

第一个命令是 [**DevCon Dp \_ add**](devcon-dp-add.md) 命令，将 WDK 中 Toaster 示例驱动程序的 INF 文件复制到驱动程序存储区，即% Windir% \\ INF 目录。 此命令包含 Toaster 示例驱动程序的 INF 文件的完全限定路径。

此命令适用于第三方 (OEM) 驱动程序和设备，但你可以使用 Toaster 示例来测试命令。

```
devcon dp_add C:\WinDDK\5322\src\general\toaster\inf\i386\toaster.inf
```

在响应中，DevCon 报告它已将 Toaster INF 文件添加到驱动程序存储区，并将其命名为 Oem2。

```
Driver Package 'oem2.inf' added.
```

在将该文件复制到驱动程序存储区之前，Windows 会将 INF 文件的二进制版本与驱动程序存储区中 INF 文件的二进制版本进行比较，以确保它不会添加重复的文件。 例如，如果重复此命令以将 Toaster 添加到驱动程序存储区，则 DevCon 不会创建新的 OEM \* .inf 文件。 它只报告现有文件的名称，如以下 DevCon 输出所示。

```
devcon dp_add C:\WinDDK\5322\src\general\toaste
r\inf\i386\toaster.inf
Driver Package 'oem2.inf' added.

devcon dp_add C:\WinDDK\5322\src\general\toaste
r\inf\i386\toaster.inf
Driver Package 'oem2.inf' added.
```

若要从驱动程序存储区中删除 Toaster 驱动程序的驱动程序包，必须使用 \* 驱动程序的 OEM .inf 文件名。 若要查找驱动程序的文件名，请使用 [**DevCon Dp \_ enum**](devcon-dp-enum.md) 命令。

以下命令列出了所有 OEM 驱动程序包及其属性。

```
devcon dp_enum
```

在响应中，DevCon 会生成以下显示内容：

```
c:\WinDDK\5322\tools\devcon\i386>devcon dp_enum
The following 3rd party Driver Packages are on this machine:
oem2.inf
    Provider: Microsoft
    Class: unknown
    Date: 12/10/2004
    Version: 2.0.1403.0
```

此信息表示 Microsoft 提供的驱动程序包使用未指定的设备类 (Toaster) 名为 OEM2。 你可以使用此信息来删除与该文件关联的驱动程序包。

以下命令将从驱动程序存储区中删除 OEM2 文件，以及其关联的预编译 INF (. pnf) 和目录 () 文件。 该命令使用 OEM \* .inf 文件名。

```
devcon dp_delete oem2.inf
```

在响应中，DevCon 显示一条消息，指示命令成功：

```
Driver Package 'oem2.inf' deleted.
```

在 \* [**DevCon Dp \_ delete**](devcon-dp-delete.md) 命令中需要提供 OEM .inf 文件名。 如果尝试使用 INF 文件的原始名称，则该命令将失败，如以下 DevCon 输出所示。

```
devcon dp_delete C:\WinDDK\5322\src\general\toa
ster.inf
Deleting the specified Driver Package from the machine failed.
devcon failed.
```

 

 





