---
title: 指定硬件 ID 的最佳做法
description: 指定硬件 ID 的最佳做法
ms.assetid: 95dcf1b1-b2cd-473f-9660-a91fda20ffc2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c670dddf5f23986a3c22f5437191db1ac8aab9d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385297"
---
# <a name="best-practices-for-specifying-hardware-ids"></a>指定硬件 ID 的最佳做法


[ **HardwareIDList** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff546121(v=vs.85))元素指定设备的一个或多个硬件标识字符串。 指定每个字符串[ **HardwareID** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff546114(v=vs.85)) XML 元素。 操作系统首先查询其标识字符串的设备，然后加载具有设备元数据包**HardwareID**与此字符串匹配的值。

每个**HardwareID**元素的值必须是[硬件 ID](hardware-ids.md)这是唯一的设备。 您必须使用[兼容 ID](compatible-ids.md)设备，如 USB 类 ID、 HID_DEVICE 或 HID_DEVICE_SYSTEM_KEYBOARD。

您必须确保每个[ **HardwareID** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff546114(v=vs.85))元数据包中指定的元素的值的准确地与相关联[硬件 ID](hardware-ids.md)的物理设备的报表。 例如，如果的硬件 ID 在一系列物理设备，设备元数据的重复使用包指定的**HardwareID**元素的值是与整个系列的设备相关联。

本部分包含有关指定的最佳做法的以下主题[硬件 Id](hardware-ids.md)对于某些类型的设备：

[Bluetooth 的设备指定硬件 Id](specifying-hardware-ids-for-a-bluetooth-device.md)

[指定计算机的硬件 Id](specifying-hardware-ids-for-a-computer.md)

[指定的多功能设备的硬件 Id](specifying-hardware-ids-for-a-multifunction-device.md)

有关格式的要求的详细信息**HardwareID** XML 元素，请参阅[ **HardwareID**](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff546114(v=vs.85))。

 

 





