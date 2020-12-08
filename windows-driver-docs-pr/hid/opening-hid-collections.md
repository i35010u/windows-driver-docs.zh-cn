---
title: 打开 HID 集合
description: 本部分介绍 HID 客户端如何与 HID 类驱动程序通信， (HIDClass) 操作设备的 HID 集合。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d1375891cb457d31061b2a0ea41ab5c1c3fc902
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832707"
---
# <a name="opening-hid-collections"></a>打开 HID 集合


本部分介绍 HID 客户端如何与 HID 类驱动程序通信， (HIDClass) 操作设备的 HID 集合。

HID 客户端可以在以下模式下运行：

-   使用模式应用程序/驱动程序
-   Kernel-Mode 驱动程序

以下各节介绍了 HID 客户端如何使用上述列表中的任一模式与 HIDClass 通信。

本部分介绍用户模式的应用程序和内核模式驱动程序如何操作 [HID 集合](hid-collections.md)。

通常，用户模式应用程序执行以下操作：

- 调用 [设备安装函数](/previous-versions/ff541299(v=vs.85)) (**SetupDi**_Xxx_ 函数) 查找和标识 HID 集合。

- 调用 CreateFile 打开 HID 集合上的文件。

- 调用 **HidD \_**<em>Xxx</em> hid 支持例程以获取 hid 集合的 [preparsed 数据](preparsed-data.md)和有关 hid 集合的信息。

- 调用 ReadFile 读取输入报告，并 WriteFile 发送输出报告。

- 调用 **HidP \_**<em>Xxx</em> hid 支持例程来解释 HID 报表。

通常，内核模式驱动程序会执行以下操作：

- 查找并标识 HID 集合

  如果驱动程序是函数或筛选器驱动程序，则它已附加到集合的设备堆栈。 但是，如果驱动程序未附加到集合的设备堆栈，则驱动程序可以 [使用即插即用通知](../kernel/using-pnp-notification.md)。

- 使用 [**IRP \_ MJ \_ CREATE**](../kernel/irp-mj-create.md) 请求打开 HID 集合

- 使用 IOCTL \_ HID \_ *XXX* 请求获取 hid 集合的 PREPARSED 数据以及有关 hid 集合的信息

- 使用 [**IRP \_ mj \_ 读取**](../kernel/irp-mj-read.md) 请求读取输入报告，并使用 [**irp \_ mj \_ 写入**](../kernel/irp-mj-write.md) 请求发送输出报告

- 调用 **HidP \_**<em>Xxx</em> hid 支持例程来解释 HID 报表

有关操作 HID 集合的详细信息，请参阅：

[找到并打开 HID 集合](finding-and-opening-a-hid-collection.md)

[强制实施适用于 HID 集合的安全读取](enforcing-a-secure-read-for-a-hid-collection.md)

[获取预分析的数据](obtaining-preparsed-data.md)

[获取集合信息](obtaining-collection-information.md)

[处理 HID 报告](handling-hid-reports.md)

[释放资源](freeing-resources.md)

 

