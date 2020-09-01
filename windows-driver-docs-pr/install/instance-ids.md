---
title: 实例 ID
description: 实例 ID 是将设备与计算机上相同类型的其他设备进行区分的设备标识字符串。
ms.assetid: 093063a6-1855-4e36-9465-1eedaa3cd0f9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5dc51af17d0eb3524b74d1a6c7ae0925ec14dbe5
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097365"
---
# <a name="instance-id"></a>实例 ID


实例 ID 是将设备与计算机上相同类型的其他设备进行区分的设备标识字符串。 实例 ID 包含序列号信息（如果基础总线支持）或某些类型的位置信息。 字符串不能包含任何 " \\ " 字符; 否则，该字符串的一般格式是特定于总线的。




实例 ID 的字符数（不包括 NULL 终止符）必须小于 MAX_DEVICE_ID_LEN。 此外，当实例 ID 连接到 [设备 id](device-ids.md) 以创建设备实例 id 时，设备 id 和实例 id 的长度将进一步受设备实例 id 的最大可能长度的约束。

设备[**DEVICE_CAPABILITIES**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构的**UniqueID**成员指示总线提供的实例 ID 在整个系统中是唯一的，如下所示：

-   如果 **UniqueID** 为 **FALSE**，则总线提供的设备实例 ID 只对设备的总线是唯一的。 即插即用 (PnP) 管理器会修改总线提供的实例 ID，并将其与相应的设备 ID 组合在一起，以创建在系统中唯一的设备实例 ID。

-   如果 **UniqueID** 为 **TRUE**，则从总线提供的设备 id 和实例 id 构成的设备实例 id 将在系统中唯一标识设备。

在系统重新启动期间，实例 ID 是永久性的。

若要获取设备的总线提供的实例 ID，请使用 [**IRP_MN_QUERY_ID**](../kernel/irp-mn-query-id.md) 请求，并将 **IdType** 成员设置为 **BusQueryInstanceID**。

 

