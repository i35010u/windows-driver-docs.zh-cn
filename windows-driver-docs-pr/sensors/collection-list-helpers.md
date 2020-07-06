---
title: 集合列表帮助程序
description: V2 传感器驱动程序使用集合列表帮助程序函数来处理传感器 \_ 集合 \_ 列表结构。
ms.assetid: 9BE06FA6-A171-4760-9D3E-C0183F3C3EFA
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 00f28a70c7f41c5466dc13f7e179f0a8086b60a3
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968236"
---
# <a name="collection-list-helpers"></a>集合列表帮助程序


V2 传感器驱动程序使用集合列表帮助程序函数来处理[**传感器 \_ 集合 \_ 列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)结构。

Helper 函数与传感器设备驱动程序软件接口（DDSI）一起使用。

**SensorCollectionGetAt**

传感器 DDSI 的使用情况

-   检索集合列表的属性键和与 PROPVARIANT 相关的属性。

注释

-   有关详细信息，请参阅[**传感器 \_ 收集 \_ 列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)。

-   有关详细信息，请参阅[**传感器 \_ 值 \_ 对**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_value_pair)。

**CollectionsListGetFillableCount**

传感器 DDSI 的使用情况

-   返回缓冲区大小（以字节为单位）。

注释

-   无。

**EvaluateActivityThresholds**

传感器 DDSI 的使用情况

-   比较新旧数据样本中的活动阈值，并返回一个布尔值。

注释

-   无。

**CollectionsListSortSubscribedActivitiesByConfidence**

传感器 DDSI 的使用情况

-   按照置信度的顺序对可能的活动的收集列表进行排序。

注释

-   无。

### <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求

**支持的最低客户端**： Windows 8。1

**支持的最低服务器**： Windows Server 2012 R2

**标头**： Sensorsutils


 

## <a name="related-topics"></a>相关主题


[帮助程序函数的封送处理](marshalling-helper-functions.md)

 

 






