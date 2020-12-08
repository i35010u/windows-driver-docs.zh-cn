---
title: BarcodeScannerTriggerReleased
description: 释放条形码扫描器触发器时，将发生 BarcodeScannerTriggerReleased 事件。
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 01ce4de2c2c214f0bb487764ce9285010e1d7244
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794315"
---
# <a name="barcodescannertriggerreleased"></a>BarcodeScannerTriggerReleased

当条形码扫描器触发器发布时发生此事件。

此事件的数据缓冲区如下所示。

## <a name="syntax"></a>语法

```cpp
typedef struct _PosEventDataHeader
{
    // Event enumeration value
    PosEventType EventType;

    // Size of buffer required to read entire event (including header)
    UINT32 DataLength;
} PosEventDataHeader;
```

下表显示此事件的数据缓冲区的内存布局。

| 内存值          | 描述                                                                |
|-----------------------|----------------------------------------------------------------------------|
| 0x00000004 | **事件**  = **PosEventType：： BarcodeScannerTriggerReleased** |
| 0x00000008 | sizeof (**PosEventDataHeader**)                                   |

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface
