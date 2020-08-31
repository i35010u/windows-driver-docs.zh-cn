---
title: 如何装载卷
description: 如何装载卷
ms.assetid: e8f39b06-9904-40e8-af52-eae310d11fa7
keywords:
- 筛选器驱动程序 WDK 文件系统，卷装入过程
- 文件系统筛选器驱动程序 WDK，卷装入过程
- 装载卷 WDK 文件系统
- 卷 WDK 文件系统，装载
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7fb90dc5c5b2c0740c1f789af9ea6a146ca499c8
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063330"
---
# <a name="how-the-volume-is-mounted"></a>如何装载卷

> [!NOTE]
> 为了获得最佳的可靠性和性能，请使用带有筛选器管理器支持的 [文件系统微筛选器驱动程序](./filter-manager-concepts.md) ，而不是使用旧的文件系统 若要将旧驱动程序移植到微筛选器驱动程序，请参阅 [迁移旧筛选器驱动程序的准则](guidelines-for-porting-legacy-filter-drivers.md)。

[识别卷](how-the-volume-is-recognized.md)后，如何装入卷取决于文件系统以及它以前是否已装载了卷。

当文件系统收到新卷的卷装入请求时，它将为卷创建 (VDO) 的卷设备对象。 VDO 包含一个 DEVICE_OBJECT 以及一个可选的文件系统定义的设备扩展。 新创建的 VDO 将形成新 (的文件系统卷堆栈的基础，或重新装载) 卷。

文件系统通过将 VDO 与卷参数块关联，为相应的存储设备对象将设置为卷参数)  (块，并在 VPB 上设置 VPB_MOUNTED 标志。

文件系统装载卷后，文件系统筛选器驱动程序可以附加到新文件系统卷堆栈的顶部。 发送到文件系统的任何 i/o 请求将首先自动发送到卷堆栈顶部的文件系统筛选器设备对象。 但是，在 i/o 管理器发送快速 i/o 分离请求以便在卷堆栈上通知驱动程序时，文件系统筛选器应只从卷堆栈分离，这是因为要删除卷。

有关示例，请参阅 [卷装入示例](volume-mount-example.md) 。

> [!NOTE]
> 卷的存储设备对象驻留在存储设备堆栈中，但它不一定是堆栈中最顶层的设备对象。 而且，即使在装入卷后，存储筛选器驱动程序仍可以附加到存储堆栈的顶部。 请注意，驱动程序编写器必须记住，当文件系统从 VDO 将 IRP 发送到存储设备堆栈时，它会将 IRP 发送到卷的存储设备对象，而不是堆栈中最顶层的设备对象。  (不过，当 i/o 管理器将 IRP 直接发送到存储堆栈（绕过文件系统）时，会将 IRP 发送到堆栈中最顶层的设备对象。 ) 