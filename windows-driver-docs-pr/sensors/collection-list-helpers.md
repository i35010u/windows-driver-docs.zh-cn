---
title: 集合列表帮助程序
description: V2 传感器驱动程序使用集合列表 helper 函数，以便使用传感器\_集合\_列表结构。
ms.assetid: 9BE06FA6-A171-4760-9D3E-C0183F3C3EFA
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9455f58104648238b26e0b1cebbd748c4f7de6e0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842535"
---
# <a name="collection-list-helpers"></a>集合列表帮助程序


V2 传感器驱动程序使用集合列表 helper 函数，以便使用[**传感器\_集合\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)结构。

Helper 函数与传感器设备驱动程序软件接口（DDSI）一起使用。

**SensorCollectionGetAt**

传感器 DDSI 的使用情况

-   检索集合列表的属性键和与 PROPVARIANT 相关的属性。

备注

-   有关详细信息，请参阅[**传感器\_收集\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)。

-   有关详细信息，请参阅[**传感器\_值\_对**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_value_pair)。

**CollectionsListGetFillableCount**

传感器 DDSI 的使用情况

-   返回缓冲区大小（以字节为单位）。

备注

-   无。

**EvaluateActivityThresholds**

传感器 DDSI 的使用情况

-   比较新旧数据样本中的活动阈值，并返回一个布尔值。

备注

-   无。

**CollectionsListSortSubscribedActivitiesByConfidence**

传感器 DDSI 的使用情况

-   按照置信度的顺序对可能的活动的收集列表进行排序。

备注

-   无。

### <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求

|                          |                        |
|--------------------------|------------------------|
| 最低受支持的客户端 | Windows 8.1            |
| 最低受支持的服务器 | Windows Server 2012 R2 |
| 标头                   | Sensorsutils         |

 

## <a name="related-topics"></a>相关主题


[封送处理 helper 函数](marshalling-helper-functions.md)

 

 






