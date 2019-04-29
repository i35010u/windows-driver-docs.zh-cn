---
title: WDI_BAND_ID
description: 本主题介绍 WDI 微型端口驱动程序的 WDI_BAND_ID 数据类型。
ms.assetid: 28E34D2C-94A5-4035-ACAA-60CECABF3A02
keywords:
- WDI_BAND_ID，WDK WDI_BAND_ID 网络驱动程序
ms.date: 11/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e8782091eaf19c4217ff0d7e57b2eb4d85895e3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391921"
---
# <a name="wdibandid"></a>WDI_BAND_ID

WDI_BAND_ID 数据类型是一个 UINT32 值，定义一个带区 id。

```c++
typedef UINT32 WDI_BAND_ID;
```

## <a name="remarks"></a>备注

可能的带区的 ID 值如下所示：

| ReplTest1 |   | 描述 |
| --- | --- | --- |
| WDI_BAND_ID_ANY | 0xFFFFFFFF | 所有带区 |
| WDI_BAND_ID_2400 | 1 | 2.4 GHz |
| WDI_BAND_ID_5000 | 2 | 5 GHz |
| WDI_BAND_ID_60000 | 3 | 60 GHz |
| WDI_BAND_ID_900 | 4 | 900 MHz |
| WDI_BAND_ID_CUSTOM_START | 0x80000000 |指定用于定义报告的 IHV 外 ID 范围的开始。 |
| WDI_BAND_ID_CUSTOM_END | 0x81000000 | 指定用于定义报告的 IHV 外 ID 范围的末尾。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |

