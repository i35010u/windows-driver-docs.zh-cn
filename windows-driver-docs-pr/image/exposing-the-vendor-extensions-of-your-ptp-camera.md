---
title: 公开 PTP 相机的供应商扩展
description: 公开 PTP 相机的供应商扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db4edc3da94bcc1a2908062d68daafaf3b5f61bf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822409"
---
# <a name="exposing-the-vendor-extensions-of-your-ptp-camera"></a>公开 PTP 相机的供应商扩展





PTP 设备可以支持供应商扩展的属性、供应商扩展的事件和供应商扩展的命令。

供应商扩展的属性和事件在 **DeviceData** INF 文件条目中列出 (参阅 [WIA 设备的 INF 文件](inf-files-for-wia-devices.md)) 的详细信息，以便驱动程序能够处理它们。 列出供应商扩展 ID 的条目是必需的。 这必须与 DeviceInfo 数据集中的 VendorExtensionID 字段匹配。 以下部分介绍了其他条目的示例。

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

 

 




