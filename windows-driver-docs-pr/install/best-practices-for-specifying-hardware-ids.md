---
title: 指定硬件 ID 的最佳做法
description: 指定硬件 ID 的最佳做法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e985fb83ea53c0d455a8b1eacb592a2fcfb0018e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839901"
---
# <a name="best-practices-for-specifying-hardware-ids"></a>指定硬件 ID 的最佳做法


[**HardwareIDList**](/previous-versions/windows/hardware/metadata/ff546121(v=vs.85))元素指定设备的一个或多个硬件标识字符串。 每个字符串由 [**HardwareID**](/previous-versions/windows/hardware/metadata/ff546114(v=vs.85)) XML 元素指定。 操作系统首先向设备查询其标识字符串，然后加载其 **HardwareID** 值与此字符串匹配的设备元数据包。

每个 **HardwareID** 元素值都必须是设备独有的 [硬件 ID](hardware-ids.md) 。 不得使用设备的 [兼容 ID](compatible-ids.md) ，如 USB 类 id、"HID_DEVICE" 或 "HID_DEVICE_SYSTEM_KEYBOARD"。

必须确保元包中指定的每个 [**HardwareID**](/previous-versions/windows/hardware/metadata/ff546114(v=vs.85)) 元素都具有与物理设备所报告的 [硬件 ID](hardware-ids.md) 精确关联的值。 例如，如果在一系列物理设备上重复使用硬件 ID，则指定 **HardwareID** 元素值与整个设备系列关联的设备元数据包。

本部分包括以下有关为某些类型的设备指定 [硬件 id](hardware-ids.md) 的最佳实践的主题：

[指定蓝牙设备的硬件 ID](specifying-hardware-ids-for-a-bluetooth-device.md)

[指定计算机的硬件 ID](specifying-hardware-ids-for-a-computer.md)

[指定多功能设备的硬件 ID](specifying-hardware-ids-for-a-multifunction-device.md)

有关 **HardwareID** XML 元素的格式要求的详细信息，请参阅 [**HardwareID**](/previous-versions/windows/hardware/metadata/ff546114(v=vs.85))。

 

