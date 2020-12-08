---
title: 强制实施适用于 HID 集合的安全读取
description: 强制实施适用于 HID 集合的安全读取
keywords:
- 集合 WDK HID，安全读取
- HID 集合 WDK，安全读取
- 安全读取 WDK HID
- 受信任的安全读取 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60e0707fb646c9858f8b1481fd1e4432b2850fea
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838925"
---
# <a name="enforcing-a-secure-read-for-a-hid-collection"></a>强制实施适用于 HID 集合的安全读取





本部分介绍用户模式的应用程序或内核模式驱动程序如何强制对顶级 [HID 集合](hid-collections.md)进行 *安全读取*。

如果为集合启用了安全读取，则只有 "受信任的" 客户端 (具有 SeTcbPrivilege 特权的客户端) 可以从集合的打开文件获取输入。 默认情况下，内核模式驱动程序具有 SeTcbPrivilege 权限，但用户模式应用程序不具有。 有关如何在用户模式下获取系统特权的信息，请参阅 Microsoft Windows SDK 文档中有关授权的信息。

提供此机制主要是为了使 "受信任的" 用户模式系统组件可以在关键系统操作过程中阻止没有 SeTcbPrivilege 特权的用户模式应用程序获取集合的输入。 例如，"受信任的" 用户模式系统组件可以阻止没有 SeTcbPrivilege 权限的用户模式应用程序获取用户在登录操作过程中提供的机密信息。

"受信任的" 客户端使用 [**IOCTL \_ hid \_ 启用 \_ 安全 \_ 读取**](/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_enable_secure_read) 和 [**IOCTL \_ hid \_ 禁用 \_ 安全 \_ 读取**](/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_disable_secure_read) 请求以启用和禁用对集合的安全读取。 如果没有 SeTcbPrivilege 特权的客户端使用这些请求，则该请求不会更改集合的安全读取状态，并且 HID 类驱动程序将返回状态为 "未持有" 的状态值 \_ \_ \_ 。

为集合启用和禁用安全读取的工作方式如下：

-   HID 类驱动程序为集合的每个打开的文件维护特定于文件的安全读取计数。 HID 类驱动程序还为集合维护一个安全的读取计数，该计数是文件特定的安全读取计数之和。 创建集合时，该集合的安全读取计数初始化为零，当打开文件时，将文件的安全读取计数初始化为零。

-   当 HID 类驱动程序接收到文件的 enable 请求时，它会按1递增 (的文件的安全读取计数，并将该集合的安全读取计数增加 1) 。

-   当 HID 类驱动程序接收到文件的禁用请求时：
    -   如果文件的安全读取计数大于零，则驱动程序将按1减小 (的文件的安全读取计数，并将该集合) 的安全读取计数递减1。
    -   如果文件的安全读取计数等于零，则驱动程序不会更改安全读取计数。
-   如果集合的安全读取计数大于零，则 HID 类驱动程序会对集合强制执行安全读取。 否则，驱动程序不会为集合强制执行安全读取。

-   客户端应使用禁用请求来取消相应的启用请求。 但是，如果客户端没有这样做，则在处理对某个文件的 [**IRP \_ MJ \_ 关闭**](../kernel/irp-mj-close.md) 请求时，HID 类驱动程序会适当地递减该集合的安全读取计数。 当驱动程序处理关闭请求时，它会将该集合的安全读取计数递减为关闭的文件的安全读取计数。

 

