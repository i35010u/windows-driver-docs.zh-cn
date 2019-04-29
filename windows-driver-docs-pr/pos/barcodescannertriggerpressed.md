---
title: BarcodeScannerTriggerPressed
description: 条形码扫描程序触发器按下时，将发生 BarcodeScannerTriggerPressed 事件。
ms.assetid: 6f0a373f-bf3f-4201-9430-3474f84b9037
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9f43c8a74e6aebfc6fe81e8cca92677889f740d8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358667"
---
# <a name="barcodescannertriggerpressed"></a>BarcodeScannerTriggerPressed

条形码扫描程序触发器按下时，将发生此事件。

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

| 内存值          | 描述                                                               |
|-----------------------|---------------------------------------------------------------------------|
| 0x00000003 | **EventType** = **PosEventType::BarcodeScannerTriggerPressed** |
| 0x00000008 | sizeof(**PosEventDataHeader**)                                 |

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface.h
