---
title: BarcodeScannerErrorOccurred
description: BarcodeScannerErrorOccurred 事件发生时出现错误，例如扫描错误。
ms.assetid: 38cfbd87-0526-49d1-8580-96f4e1adf7bb
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0060519110f16262ca643b8bb4c2805ab640a534
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358775"
---
# <a name="barcodescannererroroccurred"></a>BarcodeScannerErrorOccurred

出现错误，例如扫描错误时发生此事件。

此事件的数据缓冲区是按如下所示。

## <a name="syntax"></a>语法

```cpp
// Error occurred data should fill the ReadFile buffer in this order:
//    PosBarcodeScannerErrorOccurredEventData structure (length = sizeof(PosBarcodeScannerErrorOccurredEventData))
//    Error Message (length = MessageLength)
//    Scan Data (length = ScanDataLength)
//    Scan Data Label (length = ScanDataLabelLength)

typedef struct _PosBarcodeScannerErrorOccurredEventData
{
    PosEventDataHeader Header;
    LONG IsRetriable;
    UnifiedPosErrorSeverity Severity;
    UINT32 VendorErrorCode;
    UnifiedPosErrorReason Reason;
    UINT32 ExtendedReason;
    UINT32 MessageLength;
    PosBarcodeScannerDataReceivedEventData PartialData;
} PosBarcodeScannerErrorOccurredEventData;
```

下表显示了此事件的数据缓冲区的内存布局。

| 内存值                                      | 描述                                                                                                                                        |
|---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| 0x00000006                             | **事件类型 = PosEventType::BarcodeScannerTriggerPressed**                                                                             |
| UINT32                                 | **DataLength** = sizeof(**PosBarcodeScannerErrorOccurredData**) + **MessageLength** + **ScanDataLength** + **ScanDataLabelLength**)     |
| BOOL                                   | **IsRetriable**                                                                                                                         |
| 32 位 UnifiedPosErrorSeverity         | **Severity**                                                                                                                            |
| UINT32                                 | **VendorErrorCode**                                                                                                                     |
| 32 位 UnifiedPosErrorReason           | **Reason**                                                                                                                              |
| UINT32                                 | **ExtendedReason**                                                                                                                      |
| UINT32                                 | **MessageLength**                                                                                                                       |
| PosBarcodeScannerDataReceivedEventData | **PartialData**                                                                                                                         |
| UINT32                                 | **EventType**未指定                                                                                                             |
| UINT32                                 | **DataLength** = sizeof(**PosBarcodeScannerDataRecievedEventData**) + **MessageLength** + **ScanDataLength** + **ScanDataLabelLength**) |
| UINT32                                 | **数据类型**未指定                                                                                                              |
| UINT32                                 | **ScanDataLength**                                                                                                                      |
| UINT32                                 | **ScanDataLabelLength**                                                                                                                 |
| byte \[\]                              | **MessageLength**消息的字节                                                                                                      |
| byte \[\]                              | **ScanDataLength**标签数据的字节                                                                                                  |
| byte \[\]                              | **ScanDataLabelLength**扫描数据的字节                                                                                              |



## <a name="remarks"></a>备注

如果扫描出错，并获取一些扫描数据，事件数据包含部分扫描数据。

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface.h
