---
title: 集合列表帮助程序
description: 集合列表帮助程序函数由 v2 传感器驱动程序，用于处理传感器\_集合\_列表结构。
ms.assetid: 9BE06FA6-A171-4760-9D3E-C0183F3C3EFA
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: ab9ca2c16d5d79554bb004c382018b71ee5a561f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565308"
---
# <a name="collection-list-helpers"></a>集合列表帮助程序


集合列表帮助程序函数的 v2 传感器驱动程序，用来处理[**传感器\_集合\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)结构。

传感器设备驱动程序软件接口 (DDSI) 一起使用的帮助器函数。

**SensorCollectionGetAt**

通过传感器 DDSI 的使用情况

-   检索属性键和 PROPVARIANT 相关属性的集合列表。

备注

-   请参阅[**传感器\_集合\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)有关详细信息。

-   请参阅[**传感器\_值\_对**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_value_pair)有关详细信息。

**CollectionsListGetFillableCount**

通过传感器 DDSI 的使用情况

-   返回缓冲区大小，以字节为单位。

备注

-   无。

**EvaluateActivityThresholds**

通过传感器 DDSI 的使用情况

-   将在旧的和新的数据示例中，活动阈值进行比较并返回一个布尔值。

备注

-   无。

**CollectionsListSortSubscribedActivitiesByConfidence**

通过传感器 DDSI 的使用情况

-   置信度级别的顺序中的可能活动集合列出了排序。

备注

-   无。

### <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求

|                          |                        |
|--------------------------|------------------------|
| 最低受支持的客户端 | Windows 8.1            |
| 最低受支持的服务器 | Windows Server 2012 R2 |
| Header                   | Sensorsutils.h         |

 

## <a name="related-topics"></a>相关主题


[帮助器函数的封送处理](marshalling-helper-functions.md)

 

 






