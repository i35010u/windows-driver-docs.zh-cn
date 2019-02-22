---
title: COM 端口数据库
description: COM 端口数据库
ms.assetid: c9baf147-6e33-4ed2-b682-c141938eb0da
keywords:
- COM 端口 WDK 串行设备
- 串行设备 WDK、 COM 端口
- COM 端口数据库 WDK 串行设备
- COM 端口号 WDK 串行设备
- 端口号 WDK 串行设备
- 释放端口号
- 当前端口号使用 WDK 串行设备
- 大小 WDK COM 端口数据库
- 调整大小的 COM 端口数据库
- 数据库 WDK COM 端口数据库
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9f52c2eb04737182a73deb4321afffe80ef04a9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546739"
---
# <a name="com-port-database"></a>COM 端口数据库





系统提供的 COM 端口数据库对话的 COM 端口号，通过使用[COM 端口](configuration-of-com-ports.md)系统上安装。 Microsoft Windows 提供了此组件以便安装 COM 端口和，具体而言，若要确保每个端口号赋予，最多一个端口。 该组件包含的数据库和一个包含安装软件来访问数据库的调用的函数库。 COM 端口的所有系统提供安装程序都使用 COM 端口数据库获取 COM 端口号。 尽管不是插必需的但所有供应商提供的安装程序还应使用 COM 端口数据库以获取 COM 端口号。

以下主题介绍如何使用 COM 端口数据库以获取 COM 端口号：

COM 端口数据库的结构

打开和关闭的 COM 端口数据库

确定当前的使用情况的 COM 端口号

获取并释放 COM 端口号

调整大小的 COM 端口数据库

有关支持的 COM 端口数据库的例程的信息，请参阅[COMPort 数据库支持例程](https://msdn.microsoft.com/library/windows/hardware/ff546483)。

若要在安装程序中调用这些例程，链接到安装程序*msports.lib*，提供与 Windows Driver Kit (WDK)。

### <a name="structure-of-the-com-port-database"></a>COM 端口数据库的结构

COM 端口数据库包含一个元素的数组，其中每个指示是否正在使用 COM 端口号。 第一个数组元素对应于 COM1，第二个对应于 COM2，依此类推。 但是，数据库不包含设备分配给定的端口号的任何信息。 数据库的大小等于数据库当前进行仲裁的端口号的数目。 最小数目的数据库进行仲裁的端口号是 COMDB\_最小\_端口\_仲裁和它进行仲裁的最大数目是 COMDB\_MAX\_端口\_仲裁。 可以使用增加数据库的大小[ **ComDBResizeDatabase** ](https://msdn.microsoft.com/library/windows/hardware/ff546480)例程。

### <a name="opening-and-closing-the-com-port-database"></a>打开和关闭的 COM 端口数据库

使用 COM 端口数据库之前，客户端必须打开数据库通过调用[ **ComDBOpen** ](https://msdn.microsoft.com/library/windows/hardware/ff546476)例程，以获取到数据库句柄。 通过在任何连续数据库访问权限的互相排斥保护数据库。 但是，数据库无法打开供独占使用，并且其状态可能对数据库的非重复访问之间会动态变化。

### <a name="determining-the-current-usage-of-com-port-numbers"></a>确定当前的使用情况的 COM 端口号

在打开 COM 端口数据库之后，客户端可以确定哪些 COM 端口号已在使用通过调用[ **ComDBGetCurrentPortUsage** ](https://msdn.microsoft.com/library/windows/hardware/ff546474)例程。

将客户端通常执行以下任务：

1.  调用以确定多少端口号当前正在仲裁在数据库中的例程。

2.  第二次调用该例程返回调用方分配的位数组或字节数组中每一位或字节其中指定对应的端口号是否正在使用端口号使用情况信息。

如果在数据库中的所有端口号都正在使用，或者目前已没有合适的端口号，客户端可以调整数据库的大小。 有关详细信息，请参阅重设大小 COM 端口数据库。

### <a name="obtaining-and-releasing-a-com-port-number"></a>获取并释放 COM 端口号

客户端可以通过调用以下例程之一获取 COM 端口号：

-   [**ComDBClaimNextFreePort**](https://msdn.microsoft.com/library/windows/hardware/ff546469)，哪些声明最低可用的端口号。

-   [**ComDBClaimPort**](https://msdn.microsoft.com/library/windows/hardware/ff546472)，它会尝试声明特定的端口号。

C*laiming* COM 端口号 COM 端口数据库中的记录为"使用中"的端口号。

客户端通过调用来释放端口号[ **ComDBReleasePort** ](https://msdn.microsoft.com/library/windows/hardware/ff546477)例程。

### <a name="resizing-the-com-port-database"></a>调整大小的 COM 端口数据库

客户端可以重设大小的 COM 端口数据库通过调用[ **ComDBResizeDatabase** ](https://msdn.microsoft.com/library/windows/hardware/ff546480)例程。 客户端只能增加由整数数据库的大小为 1024年的倍数。 数据库的最大大小是 COMDB\_最大\_端口\_仲裁。

 

 




