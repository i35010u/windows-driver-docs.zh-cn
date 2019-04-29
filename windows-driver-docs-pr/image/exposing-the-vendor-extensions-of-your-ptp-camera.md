---
title: 公开 PTP 相机的供应商扩展
description: 公开 PTP 相机的供应商扩展
ms.assetid: b3a8b70b-c7ac-4e45-97bb-9b58e013100d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e8c38cb4457a99f093d5c0a2f973b8872459cc8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373123"
---
# <a name="exposing-the-vendor-extensions-of-your-ptp-camera"></a>公开 PTP 相机的供应商扩展





PTP 设备可以支持供应商扩展属性、 供应商扩展事件和供应商扩展的命令。

中列出了供应商扩展属性和事件**DeviceData** INF 文件条目 (请参阅[WIA 设备 INF 文件](inf-files-for-wia-devices.md)有关详细信息)，因此驱动程序是如何处理它们。 列出供应商扩展 ID 的条目是必需的。 它必须匹配在 DeviceInfo 数据集中的 VendorExtensionID 字段。 其他条目的示例如下所示，以下各节中所述。

```INF
[DeviceData]
VendorExtID=0x12345678
PropCode="0xD001,0xD002,0xD003"
PropCodeD001="0x00009802,VendorProperty1"
PropCodeD002="0x00009803,VendorProperty2"
PropCodeD003="0x00009804,VendorProperty3"
EventCode="0xC001,0xC002"
EventCodeC001={191D9AE7-EE8C-443c-B3E8-A3F87E0CF3CC}
EventCodeC002={8162F5ED-62B7-42c5-9C2B-B1625AC0DB93}
```

 

 




