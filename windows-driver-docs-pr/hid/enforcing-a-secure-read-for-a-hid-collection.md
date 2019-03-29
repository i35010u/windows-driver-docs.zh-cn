---
title: 强制实施适用于 HID 集合的安全读取
description: 强制实施适用于 HID 集合的安全读取
ms.assetid: be3c7d1b-195c-4b7f-a404-070b3b265333
keywords:
- WDK HID，安全的集合读取
- HID 的集合 WDK，安全读取
- 安全读取 WDK HID
- 受信任的安全读取 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5ea56c054f43955a4299ef6ee06b4f80228964b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563637"
---
# <a name="enforcing-a-secure-read-for-a-hid-collection"></a>强制实施适用于 HID 集合的安全读取





本部分介绍了如何强制用户模式应用程序或内核模式驱动程序可以*安全读取*为顶级[HID 集合](hid-collections.md)。

如果为集合启用了安全读取，只有"受信任的"客户端 （即带有 SeTcbPrivilege 权限） 可以从打开的文件的集合获取输入。 内核模式驱动程序具有 SeTcbPrivilege 权限默认情况下，但用户模式应用程序不这样做。 有关如何获取在用户模式下的系统权限的信息，请参阅 Microsoft Windows SDK 文档中的授权有关的信息。

此机制被提供主要，以便"受信任的"用户模式系统组件可以防止用户模式下的应用程序无需 SeTcbPrivilege 权限在关键系统操作期间集合中获取输入。 例如，"受信任的"用户模式系统组件可以防止没有 SeTcbPrivilege 特权的用户模式应用程序获取一个用户在登录操作期间提供的机密信息。

"受信任的"客户端使用[ **IOCTL\_HID\_启用\_SECURE\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff541081)并[ **IOCTL\_HID\_禁用\_SECURE\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff541077)集合读取请求，以启用和禁用的安全。 如果无需 SeTcbPrivilege 权限的客户端使用这些请求，请求不会更改集合的安全读取的状态并且 HID 类驱动程序返回的状态的状态值\_特权\_不\_保持。

启用和禁用安全可以按以下方式读取集合中的工作原理：

-   HID 类驱动程序保留每个打开的文件集合的一个特定于文件的安全读取的计数。 HID 类驱动程序还维护该集合，这是特定于文件的安全读取计数之和的安全读取的计数。 安全读取计数的集合初始化为零当创建集合，并且一种安全的读取计数初始化文件零时打开文件。

-   当 HID 类驱动程序收到启用请求的文件时，它的文件的安全读取的计数递增 1 （和找不到安全的读取的计数递增 1）。

-   当 HID 类驱动程序收到禁用请求的文件：
    -   如果安全读取的文件计数大于零，驱动程序递减 1 安全读取的文件 （和安全读取计数找不到 1 递减） 的计数。
    -   如果该文件的安全读取的计数为零，则驱动程序不会更改安全读取的计数。
-   如果集合的安全读取的计数大于零，HID 类驱动程序强制实施安全读取的集合。 否则，该驱动程序不强制安全读取的集合。

-   客户端应使用禁用请求来取消相应的启用请求。 但是，如果客户端不会执行此操作，HID 类驱动程序相应地减少安全阅读集合计数处理时[ **IRP\_MJ\_关闭**](https://msdn.microsoft.com/library/windows/hardware/ff550720)文件的请求。 当驱动程序处理关闭请求，它是安全的递减读取找不到正在关闭该文件的安全读取计数的计数。

 

 




