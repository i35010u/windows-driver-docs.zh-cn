---
title: WIA_IPS_COLOR_DROP_MULTI
description: 当可以同时拖出多个颜色时，将使用 WIA_IPS_COLOR_DROP_MULTI 属性进行报告。
keywords:
- WIA_IPS_COLOR_DROP_MULTI 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_COLOR_DROP_MULTI
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0e2441a68c7fb508fdba353dbfdc5213be6ac461
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184017"
---
# <a name="wia_ips_color_drop_multi"></a>WIA \_ IPS \_ 颜色 \_ 删除 \_ 多

**WIA \_ ip \_ 颜色 \_ DROP \_ 多**属性用于报告可以同时拖出多个颜色的情况。 例如，如果此属性的值为2，则该应用程序可以将**wia \_ ip 颜色 " \_ \_ 删除 \_ 红色**"、" **wia ip 颜色"、"wia ip 颜色"、"wia ip \_ \_ 颜色 \_ \_ **"、"wia ip 颜色" 和 "wia ip 颜色" 属性设置为包含每两个值的枚举，这说明了** \_ \_ \_ **

此属性由 WIA 迷你驱动程序初始化和维护。

属性类型： VT \_ UI4

有效值： WIA " \_ \_ 无"

访问权限：只读

## <a name="remarks"></a>备注

此属性对所有可编程的图像数据源项有效，包括 \_ \_ \_ \_ 仅当支持 [**wia \_ Ip \_ 颜色 \_ DROP**](./wia-ips-color-drop.md) 属性时，平板 (WIA 类别平板) 和送纸器 (wia 类别送) 纸器。

## <a name="requirements"></a>要求

| &nbsp; | &nbsp; |
| --- |:--- |
| **标头** | Wiadef (包含 Wiadef)  |