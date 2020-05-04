---
title: 设备实例 ID
description: 设备实例 ID 是系统提供的设备标识字符串，用于在系统中唯一标识设备。
ms.assetid: 578973f4-463f-4707-8dc3-dff27b3d3052
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 714f0771a34091002ebfdf5941c09c55e1f45237
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "72007624"
---
# <a name="device-instance-id"></a>设备实例 ID


设备实例 ID 是系统提供的设备标识字符串，用于在系统中唯一标识设备。 即插即用 (PnP) 管理器将设备实例 ID 分配给系统[设备树](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)中的每个设备节点 (devnode  )。




此字符串的格式由[实例 ID](instance-ids.md) 连接到[设备 ID](device-ids.md) 组成，如下所示：

`<device-ID>\<instance-specific-ID>`

设备实例 ID 的字符数（不包括 NULL 终止符）必须少于 MAX_DEVICE_ID_LEN。 此约束适用于所有字段和“\\”字段分隔符（分隔设备 ID  与实例特定 ID  字段）的长度总和。

设备实例 ID 在系统重启后保持不变。

下面举个例子，一个实例 ID ("1&08") 连接到一个 PCI 设备的设备 ID：

`PCI\VEN_1000&DEV_0001&SUBSYS_00000000&REV_02\1&08`

 

 





