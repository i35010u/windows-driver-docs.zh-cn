---
title: WDI_BAND_ID
description: 本主题介绍 WDI 微型端口驱动程序的 WDI_BAND_ID 数据类型。
ms.assetid: 28E34D2C-94A5-4035-ACAA-60CECABF3A02
keywords:
- WDI_BAND_ID，WDK WDI_BAND_ID 网络驱动程序
ms.date: 11/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18e4555ee2153c12c29bbed91fa79dc74801587b
ms.sourcegitcommit: 74a8dc9ef1da03857dec5cab8d304e2869ba54a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90759782"
---
# <a name="wdi_band_id"></a>WDI_BAND_ID

WDI_BAND_ID 数据类型是一个定义带区 ID 的 UINT32 值。

```c++
typedef UINT32 WDI_BAND_ID;
```

## <a name="remarks"></a>备注

可能的带区 ID 值如下所示：

| “属性” | “值”  | 描述 |
| --- | --- | --- |
| WDI_BAND_ID_ANY | 0xFFFFFFFF | 所有带区 |
| WDI_BAND_ID_2400 | 1 | 2.4 GHz |
| WDI_BAND_ID_5000 | 2 | 5 GHz |
| WDI_BAND_ID_60000 | 3 | 60 GHz |
| WDI_BAND_ID_900 | 4 | 900 MHz |
| WDI_BAND_ID_CUSTOM_START | 0x80000000 |指定用于定义 IHV 报告的带区 ID 的范围的开始时间。 |
| WDI_BAND_ID_CUSTOM_END | 0x81000000 | 指定范围的结束，该范围用于定义由 IHV 报告的带区 ID。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 10

**支持的最低服务器**： Windows server 2016

**标头**： Wditypes. hpp


