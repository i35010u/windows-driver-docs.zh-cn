---
title: BarcodeScannerTriggerPressed
description: 按下条形码扫描器触发器时，将发生 BarcodeScannerTriggerPressed 事件。
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4a1f6e5f173a1c239c0c894b40f48a95ec05822a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806019"
---
# <a name="barcodescannertriggerpressed"></a>BarcodeScannerTriggerPressed

按下条形码扫描器触发器时发生此事件。

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

| 内存值          | 描述                                                               |
|-----------------------|---------------------------------------------------------------------------|
| 0x00000003 | **事件**  = **PosEventType：： BarcodeScannerTriggerPressed** |
| 0x00000008 | sizeof (**PosEventDataHeader**)                                  |

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface
