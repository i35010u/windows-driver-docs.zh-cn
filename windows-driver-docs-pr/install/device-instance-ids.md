---
title: 设备实例 ID
description: 设备实例 ID 是系统提供的设备标识字符串，用于在系统中唯一标识设备。
ms.assetid: 578973f4-463f-4707-8dc3-dff27b3d3052
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 714f0771a34091002ebfdf5941c09c55e1f45237
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007624"
---
# <a name="device-instance-id"></a>设备实例 ID


设备实例 ID 是系统提供的设备标识字符串，用于在系统中唯一标识设备。 即插即用（PnP）管理器为系统[设备树](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)中的每个设备节点（*devnode*）分配一个设备实例 ID。




此字符串的格式由连接到[设备 ID](device-ids.md)的[实例 ID](instance-ids.md)组成，如下所示：

`<device-ID>\<instance-specific-ID>`

设备实例 ID 的字符数（不包括 NULL 终止符）必须小于 MAX_DEVICE_ID_LEN。 此约束适用于*设备 ID*和*实例特定 ID*字段之间所有字段的长度与 "\\" 字段分隔符之和。

在系统重新启动期间，设备实例 ID 是永久性的。

下面是连接到 PCI 设备的设备 ID 的实例 ID （"1 & 08"）的示例：

`PCI\VEN_1000&DEV_0001&SUBSYS_00000000&REV_02\1&08`

 

 





