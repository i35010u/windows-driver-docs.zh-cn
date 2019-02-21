---
title: BarcodeScannerImagePreviewReceived
description: 当设备接收扫描的位图图像，BarcodeScannerImagePreviewReceived 事件时发生。
ms.assetid: ec05bffb-95e6-4d9c-b632-adee1cbd5bad
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: ad80780dcb8af4d32b58732833c2dd0af62cadf1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542211"
---
# <a name="barcodescannerimagepreviewreceived"></a>BarcodeScannerImagePreviewReceived

当设备接收扫描的位图图像时，将发生此事件。

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

typedef struct _PosEventDataHeader PosBarcodeScannerImagePreviewEventData;
```

下表显示了此事件的数据缓冲区的内存布局。

| 内存值                                 | 描述                                                                                                 |
|----------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| 0x00000007                        | **EventType** = **PosEventType::BarcodeScannerImagePreviewReceived**                            |
| 0x00000008 + 图像数据的长度 | sizeof (**PosBarcodeScannerImagePreviewEventData**) + 预览以字节为单位的数据的图像的大小 |
| 图像数据                        | 预览图像数据                                                                           |

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface.h
