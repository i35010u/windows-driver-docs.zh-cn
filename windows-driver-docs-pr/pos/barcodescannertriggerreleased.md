---
title: BarcodeScannerTriggerReleased
description: BarcodeScannerTriggerReleased 事件发生时发布条形码扫描程序触发器。
ms.assetid: 49b655c3-2652-4225-ba4c-5404da672b8e
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: f110d73a2436a64a43ec2f17c550dc3b5366a67d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554759"
---
# <a name="barcodescannertriggerreleased"></a>BarcodeScannerTriggerReleased

条形码扫描程序触发器发布时，将发生此事件。

此事件的数据缓冲区是按如下所示。

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

下表显示了此事件的数据缓冲区的内存布局。

| 内存值          | 描述                                                                |
|-----------------------|----------------------------------------------------------------------------|
| 0x00000004 | **EventType** = **PosEventType::BarcodeScannerTriggerReleased** |
| 0x00000008 | sizeof(**PosEventDataHeader**)                                  |

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface.h
