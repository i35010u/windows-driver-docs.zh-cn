---
title: 数据范围属性
description: 数据范围属性
ms.assetid: 84bdd151-a034-445e-9f6d-19940e32b2c1
keywords:
- 数据交集处理程序 WDK 音频，数据范围属性
- 数据范围 WDK 音频，属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd9705672e065dfa40c897a66cb95924ebe1a795
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208163"
---
# <a name="data-range-properties"></a>数据范围属性


## <span id="data_range_properties"></span><span id="DATA_RANGE_PROPERTIES"></span>


数据范围不仅用于数据交集，还可以作为设备属性进行访问 (参阅 [固定数据范围和交集属性](pin-data-range-and-intersection-properties.md)) 。 出于此原因，适配器驱动程序（其数据交集处理程序负责处理其引脚上的所有格式协商）应仍包含一组完整的数据范围。 数据范围应尽可能接近于适配器的数据交集处理程序中所述的数据格式首选项。

可以通过以下属性访问 pin 的数据范围：

[**KSPROPERTY \_ PIN \_ DATARANGES**](../stream/ksproperty-pin-dataranges.md)

[**KSPROPERTY \_ PIN \_ CONSTRAINEDDATARANGES**](../stream/ksproperty-pin-constraineddataranges.md)

这两个属性分别指定 pin 的静态数据范围和约束的数据范围。

受约束的数据范围提供有关设备当前功能的更精确信息，因为它们会动态更新，以考虑已分配给其他用途的任何机载资源。 相比之下，静态数据范围可能会不准确地报告依赖于不再可用的资源的硬件功能。

在当前 PortCls 实现中，端口驱动程序中的默认数据交集处理程序只使用适配器的静态数据范围。

 

