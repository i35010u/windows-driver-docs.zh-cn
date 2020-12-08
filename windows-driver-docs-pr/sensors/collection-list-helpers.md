---
title: 集合列表帮助程序
description: V2 传感器驱动程序使用集合列表帮助程序函数来处理传感器 \_ 集合 \_ 列表结构。
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: f2619efa7de5be93f8e98c2f9acbe42b447ce2b3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831059"
---
# <a name="collection-list-helpers"></a>集合列表帮助程序


V2 传感器驱动程序使用集合列表帮助程序函数来处理 [**传感器 \_ 集合 \_ 列表**](/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list) 结构。

Helper 函数与传感器设备驱动程序软件接口一起使用 (DDSI) 。

**SensorCollectionGetAt**

传感器 DDSI 的使用情况

-   检索集合列表的属性键和与 PROPVARIANT 相关的属性。

注释

-   有关详细信息，请参阅 [**传感器 \_ 收集 \_ 列表**](/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list) 。

-   有关详细信息，请参阅 [**传感器 \_ 值 \_ 对**](/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_value_pair) 。

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

 

