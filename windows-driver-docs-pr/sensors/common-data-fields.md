---
title: 常见数据字段
description: 本主题显示了所有特定于传感器的数据字段中包含的常见数据字段。
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2da157238258a9e2b562563c0a537b32759cf69d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812369"
---
# <a name="sensor-data-fields"></a>传感器数据字段

*传感器数据字段* 表示传感器可以提供的特定类型的信息。 报告数据时，值被视为包含在 *数据字段* 中。 相关数据字段的集合构成了 *数据报表*。 数据报表在 SENSOR_COLLECTION_LIST 结构中打包在一起。 每个数据报表必须包含至少一个有效的数据字段和一个标识数据报表创建时间的时间戳。 时间戳由 PKEY_SensorData_Timestamp 属性键表示。 数据字段的示例是加速感应的 x、y、z 加速度值。 每个数据字段由 **PROPERTYKEY** 常量标识。

## <a name="common-data-fields"></a>常见数据字段

下面的字段类型包含在所有特定于传感器的数据字段中。

客户端可以使用 ReadFile 函数从这些数据字段中检索信息。

有关 "类型" 列中显示的类型的详细信息，请参阅 [PROPVARIANT 结构](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)。

|属性键|类型|必需/可选|说明|
| --- | --- | --- | --- |
|PKEY_SensorData_Timestamp|VT_FILETIME|必须|由驱动程序计算的文件时间（UTC 格式）。 类扩展 (CX) 提供帮助程序函数，用于将计时周期转换为 FILETIME，使远程系统不必与系统时钟同步。|

## <a name="related-topics"></a>相关主题

[PROPVARIANT 结构](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)
