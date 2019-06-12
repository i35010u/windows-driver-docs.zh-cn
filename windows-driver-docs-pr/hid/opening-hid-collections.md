---
title: 打开 HID 集合
description: 本部分介绍 HID 客户端之间的通信方式的 HID 类驱动程序 (HIDClass) 运行 HID 设备的集合。
ms.assetid: 97550D1D-2C37-4996-8522-DB18B1AA3C4A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4be15d880b997d6bff9ab3b1c6637270212955a1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364614"
---
# <a name="opening-hid-collections"></a>打开 HID 集合


本部分介绍 HID 客户端之间的通信方式的 HID 类驱动程序 (HIDClass) 运行 HID 设备的集合。

HID 客户端可以运行在以下模式：

-   使用模式应用程序/驱动程序
-   Kernel-Mode Driver

以下各节确定 HID 客户端之间的通信方式 HIDClass 上述列表中使用任何一种模式。

本部分介绍了用户模式应用程序和内核模式驱动程序工作方式[HID 集合](hid-collections.md)。

一般情况下，在用户模式应用程序执行以下任务：

- 调用[设备安装函数](https://msdn.microsoft.com/library/windows/hardware/ff541299)(**SetupDi * * * Xxx*函数) 来查找和标识 HID 集合。

- 调用 CreateFile 打开 HID 集合上的文件。

- 调用**HidD\_** <em>Xxx</em> HID 支持例程，获取 HID 集合[preparsed 数据](preparsed-data.md)和 HID 集合有关的信息。

- 调用读取输入的报告 ReadFile 和 WriteFile 发送输出报告。

- 调用**HidP\_** <em>Xxx</em> HID 支持例程来解释 HID 报表。

一般情况下，内核模式驱动程序执行以下任务：

- 查找和标识 HID 集合

  如果该驱动程序是一个函数或筛选器驱动程序，它是已附加到集合的设备堆栈。 但是，如果该驱动程序未附加到集合的设备堆栈，该驱动程序可以[使用插通知](https://msdn.microsoft.com/library/windows/hardware/ff565480)。

- 使用[ **IRP\_MJ\_创建**](https://msdn.microsoft.com/library/windows/hardware/ff550729)请求打开 HID 集合

- 使用 IOCTL\_HID\_*Xxx*请求以获取 HID 集合 preparsed 的数据和有关 HID 收集的信息

- 使用[ **IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff550794)请求以便读取输入的报表和[ **IRP\_MJ\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff550819)发送输出的报表的请求

- 调用**HidP\_** <em>Xxx</em> HID 支持例程来解释 HID 报表

有关运行 HID 集合的详细信息，请参阅：

[查找和打开 HID 集合](finding-and-opening-a-hid-collection.md)

[强制实施安全读取 HID 集合](enforcing-a-secure-read-for-a-hid-collection.md)

[获取 Preparsed 的数据](obtaining-preparsed-data.md)

[获取集合的信息](obtaining-collection-information.md)

[处理 HID 报表](handling-hid-reports.md)

[释放资源](freeing-resources.md)

 

 




