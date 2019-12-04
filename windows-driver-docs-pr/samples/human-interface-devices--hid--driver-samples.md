---
title: 人机接口设备 (HID) 驱动程序示例
description: 此目录中的驱动程序示例提供了为设备编写自定义 HID 驱动程序的起点。
ms.assetid: 38C52EAD-9DC6-4575-A9FF-1472FDDC2702
ms.date: 11/19/2019
ms.localizationpriority: medium
ms.openlocfilehash: a2f4a0f7d636ae025281da12b703d136439fa02f
ms.sourcegitcommit: 30fa63ad13fd5e2e883b76a44f0703e01049ffa1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74735259"
---
# <a name="human-interface-devices-hid-driver-samples"></a>人机接口设备 (HID) 驱动程序示例

此目录中的驱动程序示例提供了为设备编写自定义 HID 驱动程序的起点。

| 示例 | 描述 |
| --- | --- |
| [KMDF HID 筛选器](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/kmdf-filter-driver-for-a-hid-device) | HID 设备的筛选器驱动程序。 除了说明如何编写筛选器驱动程序外，此示例还演示如何使用远程 i/o 目标接口以内核模式打开 HID 集合，并发送 IOCTL 请求来设置和获取功能报告，以及应用程序如何使用 WMI 接口将命令发送到筛选器驱动程序。 |
| [HClient 应用程序](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/hclient-sample-application) | 演示如何编写与 HID 设备（符合 HID 设备类规范）进行通信的用户模式客户端应用程序。 |
| [HIDUSBFX2](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/hidusbfx2-sample-driver) | 说明如何将非 HID USB 设备映射到 HID 设备。 |
| [UMDF HID 微型驱动程序](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/hid-minidriver-sample-umdf-version-2) | 演示如何使用用户模式驱动程序框架（UMDF）编写 HID 微型驱动程序的示例。
