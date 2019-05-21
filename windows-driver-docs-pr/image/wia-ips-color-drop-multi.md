---
title: WIA_IPS_COLOR_DROP_MULTI
description: WIA_IPS_COLOR_DROP_MULTI 属性用于报告何时在同一时间，可以在多个单色删除。
keywords:
- WIA_IPS_COLOR_DROP_MULTI 成像设备
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
ms.openlocfilehash: 54be1817c00b1d4338084efd1bb8f307f751793e
ms.sourcegitcommit: 2ddaca0dbaf96076ad54d39ac1e77d91e644de67
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2019
ms.locfileid: "65958677"
---
# <a name="wiaipscolordropmulti"></a>WIA\_IPS\_颜色\_DROP\_多

**WIA\_IPS\_颜色\_DROP\_多**属性用于报告时多个是一种颜色可以同时删除。 例如，如果此属性的值为 2，则该应用程序可以设置**WIA\_IPS\_颜色\_DROP\_RED**， **WIA\_IP\_颜色\_DROP\_绿色**，并**WIA\_IP\_颜色\_蓝色**属性设置为包含每个两个值的枚举描述要删除的两种颜色。

此属性是初始化和维护的 WIA 微型驱动程序。

属性类型：VT\_UI4

有效值：WIA\_PROP\_NONE

访问权限：只读

## <a name="remarks"></a>备注

此属性仅适用于所有可编程图像数据源项，包括平板 (WIA\_类别\_平板) 和送纸器 (WIA\_类别\_送纸器) 时，才[ **WIA\_IPS\_颜色\_DROP** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-color-drop)支持属性。

## <a name="requirements"></a>要求

| &nbsp; | &nbsp; |
| --- |:--- |
| **标头** | Wiadef.h （包括 Wiadef.h） |
