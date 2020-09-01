---
title: WIA_IPS_BLANK_PAGES_SENSITIVITY
description: WIA_IPS_BLANK_PAGES_SENSITIVITY 属性用于将空白页面检测触发器更改为设备支持的最低和最高敏感度之间的较低或较高的值。
keywords:
- WIA_IPS_BLANK_PAGES_SENSITIVITY 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_BLANK_PAGES_SENSITIVITY
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8559b0c446b697772fecbec95d99ad6ba6336745
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189565"
---
# <a name="wia_ips_blank_pages_sensitivity"></a>WIA \_ IP \_ 空白 \_ 页 \_ 敏感度

" **WIA \_ ip \_ 空白 \_ 页 \_ 敏感度** " 属性用于将空白页面检测触发器更改为设备支持的最低和最高敏感度之间的较小值和最大值。

WIA 小型驱动程序可以在内部为每个 [**wia \_ IPA \_ 数据 \_ 类型**](./wia-ipa-datatype.md) 和 [**wia \_ IPA \_ 深度**](./wia-ipa-depth.md) 支持的颜色模式组合使用不同的敏感度值。

此属性由 WIA 迷你驱动程序初始化和维护。

属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 范围

访问权限：读写

## <a name="remarks"></a>备注

此属性是可选的，并且 (仅 \_ \_ 在支持 wia 类别进纸器) 的情况下，仅当支持 [**wia \_ ip \_ 空 \_ 页面**](./wia-ips-blank-pages.md) 时，至少与 **wia \_ 空白 \_ 页 \_ 检测 \_ 禁用**的值相同时，此属性才有效。

## <a name="requirements"></a>要求

| &nbsp; | &nbsp; |
| --- |:--- |
| **标头** | Wiadef (包含 Wiadef)  |