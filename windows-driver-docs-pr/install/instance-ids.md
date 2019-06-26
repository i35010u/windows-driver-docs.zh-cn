---
title: 实例 ID
description: 实例 ID 是相同类型的计算机上的其他设备区分开来设备的设备标识字符串。
ms.assetid: 093063a6-1855-4e36-9465-1eedaa3cd0f9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 353527552205fa383d1b13a35975acad465416a7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370927"
---
# <a name="instance-id"></a>实例 ID


实例 ID 是相同类型的计算机上的其他设备区分开来设备的设备标识字符串。 实例 ID 包含序列号的信息，如果支持基础总线或某种类型的位置信息。 字符串不能包含任何"\\"字符; 否则为泛型字符串的格式是特定于总线的。




实例 ID，不包括 NULL 终止符的字符数必须小于 MAX_DEVICE_ID_LEN。 此外，实例 ID 连接到[设备 ID](device-ids.md)若要创建一个设备实例 ID，设备 ID 和实例 ID 的长度受到进一步的限制的设备实例 ID 的最大可能长度

**UniqueID**的成员[ **DEVICE_CAPABILITIES** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)结构的设备将指示是否总线提供的实例 ID 是唯一在系统中，按如下所示：

-   如果**UniqueID**是**FALSE**，设备的总线提供的实例 ID 是唯一的设备的总线仅。 插即用 (PnP) 管理器修改总线提供的实例 ID，并将其组合使用相应设备 ID、 创建在系统中是唯一的设备实例 ID。

-   如果**UniqueID**是**TRUE**，从总线提供设备 ID 和实例 ID 格式正确的设备实例 ID 唯一地标识系统中的设备。

在系统重启后，实例 ID 是持久性的。

若要获取设备的总线提供的实例 ID，请使用[ **IRP_MN_QUERY_ID** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)请求并设置**Parameters.QueryId.IdType**成员添加到**BusQueryInstanceID**。

 

 





