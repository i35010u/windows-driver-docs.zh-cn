---
title: 流量类优先级分配
description: 流量类优先级分配
ms.assetid: 846AC7E6-28D9-4610-9493-BE547869AB15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a998ea9d816eb812ae4bd26846270e8003bd70aa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373120"
---
# <a name="traffic-class-priority-assignment"></a>流量类优先级分配


增强传输选择 (ETS) 算法指定流量类按其分配的 802.1p 优先级级别的方法。 在 IEEE 802.1Qaz 中指定 ETS 草案标准。 此标准是 framework 的 IEEE 802.1 数据中心桥接 (DCB) 接口的一部分。

NDIS 服务质量 (QoS) 通信类指定一组策略，以确定网络适配器如何处理传输，或*出口*，数据包。 下 ETS，每个流量类是分配给要传输的数据包的 IEEE 802.1p 优先级级别。 流量类可以分配给一个或多个 IEEE 802.1p 优先级级别。 但是，每个 IEEE 802.1p 优先级级别只能分配到一个通信类。

通过指定 NDIS QoS 参数[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构。 **PriorityAssignmentTable**成员包含一个数组，指定为每个流量类的分配优先级。

有关优先级级别的详细信息，请参阅[IEEE 802.1p 优先级](ieee-802-1p-priority-levels.md)。

 

 





