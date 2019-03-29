---
title: 供应商扩展的功能
description: 供应商扩展的功能
ms.assetid: 8063622e-efc4-4940-893f-2916bf297d12
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfd697a934ce8b04fe13b3d117e73b30b23ef7ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575173"
---
# <a name="vendor-extended-features"></a>供应商扩展的功能





本部分讨论供应商扩展功能 PTP 设备可以支持以下以及如何公开这些扩展：

[公开 PTP 照相机的供应商扩展](exposing-the-vendor-extensions-of-your-ptp-camera.md)

[供应商扩展属性](vendor-extended-properties.md)

[供应商扩展事件](vendor-extended-events.md)

[供应商扩展命令](vendor-extended-commands.md)

供应商扩展的属性和事件必须列在**DeviceData** INF 文件条目和事件必须在名称提供**事件**INF 文件条目 (请参阅[WIA 设备 INF 文件](inf-files-for-wia-devices.md)有关详细信息)。 列出供应商扩展 ID 的条目是必需的。 它必须匹配**VendorExtensionID** DeviceInfo 数据集字段。 其他条目的示例如下所示，以下各节中所述。

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

**请注意**   WIA 设备在 INF 文件，供应商属性名称必须是具有不含空格的单个词和组成只有字母数字值。

 

 

 




