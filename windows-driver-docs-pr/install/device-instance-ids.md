---
title: 设备实例 ID
description: 设备实例 ID 是唯一标识系统中的设备的系统提供的设备标识字符串。
ms.assetid: 578973f4-463f-4707-8dc3-dff27b3d3052
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce4f37a4f3fecfb35c3e6ae952af9492fc737601
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525619"
---
# <a name="device-instance-id"></a>设备实例 ID


设备实例 ID 是唯一标识系统中的设备的系统提供的设备标识字符串。 插即用 (PnP) 管理器将设备实例 ID 分配给设备的每个节点 (*devnode*) 中的系统[设备树](https://msdn.microsoft.com/library/windows/hardware/ff543194)。




此字符串的格式由组成[实例 ID](instance-ids.md)串联成[设备 ID](device-ids.md)，按如下所示：

`<device-ID>\<instance-specific-ID>`

设备实例 ID，不包括 NULL 终止符的字符数必须小于 MAX_DEVICE_ID_LEN。 此约束应用于所有字段的长度之和，和"\\"之间的字段分隔符*设备 ID*并*实例特定于 ID*字段。

在系统重启后，设备实例 ID 是持久性的。

下面是连接到 PCI 设备的设备 ID 的实例 ID ("1 & 08") 的示例：

`PCI\VEN_1000&DEV_0001&SUBSYS_00000000&REV_02\1&08`

 

 





