---
title: 强制实施适用于 HID 集合的安全读取
description: 强制实施适用于 HID 集合的安全读取
ms.assetid: be3c7d1b-195c-4b7f-a404-070b3b265333
keywords:
- 集合 WDK HID，安全读取
- HID 集合 WDK，安全读取
- 安全读取 WDK HID
- 受信任的安全读取 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76c7731ef49d1606bd0f398f357b591a2ec56f8b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824839"
---
# <a name="enforcing-a-secure-read-for-a-hid-collection"></a>强制实施适用于 HID 集合的安全读取





本部分介绍用户模式的应用程序或内核模式驱动程序如何强制对顶级[HID 集合](hid-collections.md)进行*安全读取*。

如果为集合启用了安全读取，则只有 "受信任的" 客户端（具有 SeTcbPrivilege 权限的客户端）才能从集合的打开文件中获取输入。 默认情况下，内核模式驱动程序具有 SeTcbPrivilege 权限，但用户模式应用程序不具有。 有关如何在用户模式下获取系统特权的信息，请参阅 Microsoft Windows SDK 文档中有关授权的信息。

提供此机制主要是为了使 "受信任的" 用户模式系统组件可以在关键系统操作过程中阻止没有 SeTcbPrivilege 特权的用户模式应用程序获取集合的输入。 例如，"受信任的" 用户模式系统组件可以阻止没有 SeTcbPrivilege 权限的用户模式应用程序获取用户在登录操作过程中提供的机密信息。

"受信任的" 客户端使用[**IOCTL\_hid\_启用\_安全\_读取**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_enable_secure_read)和[**IOCTL\_hid\_禁用\_secure\_读取**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_disable_secure_read)请求来启用和禁用对集合的安全读取。 如果没有 SeTcbPrivilege 特权的客户端使用这些请求，则请求将不会更改集合的安全读取状态，并且 HID 类驱动程序将返回状态\_\_不\_保持状态的状态值。

为集合启用和禁用安全读取的工作方式如下：

-   HID 类驱动程序为集合的每个打开的文件维护特定于文件的安全读取计数。 HID 类驱动程序还为集合维护一个安全的读取计数，该计数是文件特定的安全读取计数之和。 创建集合时，该集合的安全读取计数初始化为零，当打开文件时，将文件的安全读取计数初始化为零。

-   当 HID 类驱动程序接收到文件的 enable 请求时，它将按1增加文件的安全读取计数（并按1递增集合的安全读取计数）。

-   当 HID 类驱动程序接收到文件的禁用请求时：
    -   如果该文件的安全读取计数大于零，则驱动程序会将该文件的安全读取计数减1（并将该集合的安全读取计数减1）。
    -   如果文件的安全读取计数等于零，则驱动程序不会更改安全读取计数。
-   如果集合的安全读取计数大于零，则 HID 类驱动程序会对集合强制执行安全读取。 否则，驱动程序不会为集合强制执行安全读取。

-   客户端应使用禁用请求来取消相应的启用请求。 但是，如果客户端没有这样做，则在处理[**IRP\_MJ\_关闭**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)对文件的请求时，HID 类驱动程序会适当地减少集合的安全读取计数。 当驱动程序处理关闭请求时，它会将该集合的安全读取计数递减为关闭的文件的安全读取计数。

 

 




