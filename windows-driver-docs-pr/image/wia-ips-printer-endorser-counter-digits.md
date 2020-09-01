---
title: WIA_IPS_PRINTER_ENDORSER_COUNTER_DIGITS
description: WIA_IPS_PRINTER_ENDORSER_COUNTER_DIGITS 属性描述要为页面计数器始终打印的最小位数。
keywords:
- WIA_IPS_PRINTER_ENDORSER_COUNTER_DIGITS 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_COUNTER_DIGITS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: 951865871180b031552e782bd1bdcc5d264b7b25
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184265"
---
# <a name="wia_ips_printer_endorser_counter_digits"></a>WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 计数器 \_ 位数

**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ counter \_ ** number 属性描述为页计数器始终打印的最小位数。 其余的空数字（如果有）必须用 [**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 填充**](./wia-ips-printer-endorser-padding.md) 属性指定的填充字符来填充，如果受支持，则为零 (0) 否则为。

此属性由 WIA 迷你驱动程序初始化和维护。

属性类型： VT \_ UI4

有效值： WIA " \_ \_ 无"

访问权限：只读

## <a name="remarks"></a>备注

此属性是可选的，对于支持 [**wia \_ IPS \_ PRINTER \_ Endorser \_ 有效 \_ 格式 \_ 说明符**](./wia-ips-printer-endorser-valid-format-specifiers.md) 属性和 **wia \_ 打印 \_ 页 \_ 计数** 值的 Imprinter/Endorser 项，此属性是可选的。 实现时，属性值必须严格大于零 (0) 。

## <a name="requirements"></a>要求

| &nbsp; | &nbsp; |
| --- |:--- |
| **标头** | Wiadef (包含 Wiadef)  |