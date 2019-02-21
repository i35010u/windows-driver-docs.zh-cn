---
title: 数据范围属性
description: 数据范围属性
ms.assetid: 84bdd151-a034-445e-9f6d-19940e32b2c1
keywords:
- 数据交集处理程序 WDK 音频，数据范围属性
- 数据范围 WDK 音频属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27c0abfe3f5cb5a2cc5c7bbb6b0653fe110e961e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524050"
---
# <a name="data-range-properties"></a>数据范围属性


## <span id="data_range_properties"></span><span id="DATA_RANGE_PROPERTIES"></span>


数据区域不仅用于数据重叠，但可作为设备的属性进行访问 (请参阅[Pin 数据范围和交集属性](pin-data-range-and-intersection-properties.md))。 出于此原因，其数据交集处理程序负责在其插针上的所有格式协商的适配器驱动程序仍应包括一组完整的数据范围。 数据范围应尽可能接近地反映体现在适配器的数据交叉处理程序中的数据格式首选项。

Pin 的数据区域可以访问通过以下属性：

[**KSPROPERTY\_PIN\_DATARANGES**](https://msdn.microsoft.com/library/windows/hardware/ff565199)

[**KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES**](https://msdn.microsoft.com/library/windows/hardware/ff565195)

这两个属性分别指定 pin 的静态数据范围和受约束的数据范围。

受约束的数据区域提供更准确了解当前功能的设备，因为它们动态更新到的任何载入资源已分配用于其他用途的帐户。 相比之下，静态数据范围可能会不正确地报告依赖于不再可用的资源的硬件功能。

在当前 PortCls 实现中，端口驱动程序中的默认数据交集处理程序使用仅适配器的静态数据范围。

 

 




