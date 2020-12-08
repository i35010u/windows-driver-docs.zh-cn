---
title: BarcodeScannerImagePreviewReceived
description: 当设备接收扫描的位图图像时，将发生 BarcodeScannerImagePreviewReceived 事件。
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: e7aea3b7b180bb46a6c233acdf89b5263400fffe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794325"
---
# <a name="barcodescannerimagepreviewreceived"></a>BarcodeScannerImagePreviewReceived

当设备接收扫描的位图图像时发生此事件。

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

typedef struct _PosEventDataHeader PosBarcodeScannerImagePreviewEventData;
```

下表显示此事件的数据缓冲区的内存布局。

| 内存值                                 | 描述                                                                                                 |
|----------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| 0x00000007                        | **事件**  = **PosEventType：： BarcodeScannerImagePreviewReceived**                            |
| 0x00000008 + 图像数据的长度 | sizeof (**PosBarcodeScannerImagePreviewEventData**) + 图像预览数据的大小（以字节为单位） |
| 图像数据                        | 预览图像数据                                                                           |

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface
