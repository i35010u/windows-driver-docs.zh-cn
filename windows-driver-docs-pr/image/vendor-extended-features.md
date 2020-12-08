---
title: 供应商扩展的功能
description: 供应商扩展的功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75aecdc7d23505fc0b77fa5586480b136b6216ae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830473"
---
# <a name="vendor-extended-features"></a>供应商扩展的功能





本部分介绍了 PTP 设备可支持的供应商扩展功能，以及如何公开这些扩展：

[公开 PTP 相机的供应商扩展](exposing-the-vendor-extensions-of-your-ptp-camera.md)

[供应商扩展的属性](vendor-extended-properties.md)

[供应商扩展的事件](vendor-extended-events.md)

[供应商扩展的命令](vendor-extended-commands.md)

供应商扩展的属性和事件必须在 **DeviceData** inf 文件条目中列出，并且必须在 " **事件** inf 文件" (条目中提供一个名称。有关详细信息) ，请参阅 [用于 WIA 设备的 INF 文件](inf-files-for-wia-devices.md) 。 列出供应商扩展 ID 的条目是必需的。 这必须与 DeviceInfo 数据集中的 **VendorExtensionID** 字段匹配。 以下部分介绍了其他条目的示例。

```INF
[DeviceData]
VendorExtID=0x12345678
PropCode="0xD001,0xD002,0xD003"
PropCodeD001="0x00009802,Vendorproperty1"
PropCodeD002="0x00009803,Vendorproperty2"
PropCodeD003="0x00009804,Vendorproperty3"
EventCode="0xC001,0xC002"
EventCodeC001={191D9AE7-EE8C-443c-B3E8-A3F87E0CF3CC}
EventCodeC002={8162F5ED-62B7-42c5-9C2B-B1625AC0DB93}

[Events]
EventCodeC001="Vendorevent1",{191D9AE7-EE8C-443c-B3E8-A3F87E0CF3CC},*
EventCodeC002="Vendorevent2",{8162F5ED-62B7-42c5-9C2B-B1625AC0DB93},*
```

**注意**   在 WIA 设备的 INF 文件中，供应商属性名称必须是单个单词，无空格，并且仅包含字母数字值。

 

 

 




