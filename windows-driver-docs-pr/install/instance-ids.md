---
title: 实例 ID
description: 实例 ID 是将设备与计算机上相同类型的其他设备进行区分的设备标识字符串。
ms.assetid: 093063a6-1855-4e36-9465-1eedaa3cd0f9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d199b92b45c3df39be8d125572a11147cd480d4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837478"
---
# <a name="instance-id"></a>实例 ID


实例 ID 是将设备与计算机上相同类型的其他设备进行区分的设备标识字符串。 实例 ID 包含序列号信息（如果基础总线支持）或某些类型的位置信息。 字符串不能包含任何 "\\" 字符;否则，字符串的一般格式是特定于总线的。




实例 ID 的字符数（不包括 NULL 终止符）必须小于 MAX_DEVICE_ID_LEN。 此外，当实例 ID 连接到[设备 id](device-ids.md)以创建设备实例 id 时，设备 id 和实例 id 的长度将进一步受设备实例 id 的最大可能长度的约束。

设备的[**DEVICE_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构的**UniqueID**成员指示总线提供的实例 ID 在整个系统中是唯一的，如下所示：

-   如果**UniqueID**为**FALSE**，则总线提供的设备实例 ID 只对设备的总线是唯一的。 即插即用（PnP）管理器修改总线提供的实例 ID，并将其与相应的设备 ID 组合在一起，以创建在系统中唯一的设备实例 ID。

-   如果**UniqueID**为**TRUE**，则从总线提供的设备 id 和实例 id 构成的设备实例 id 将在系统中唯一标识设备。

在系统重新启动期间，实例 ID 是永久性的。

若要获取设备的总线提供的实例 ID，请使用[**IRP_MN_QUERY_ID**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)请求，并将**QueryId IdType**成员设置为**BusQueryInstanceID**。

 

 





