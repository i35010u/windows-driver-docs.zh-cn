---
title: BarcodeScannerErrorOccurred
description: 出现错误（例如扫描错误）时，将发生 BarcodeScannerErrorOccurred 事件。
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 827528fe6005557fb259abba72cb5a1a9f3cb82d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806027"
---
# <a name="barcodescannererroroccurred"></a>BarcodeScannerErrorOccurred

出现错误（例如扫描错误）时，将发生此事件。

此事件的数据缓冲区如下所示。

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

下表显示此事件的数据缓冲区的内存布局。

| 内存值                                      | 描述                                                                                                                                        |
|---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| 0x00000006                             | **事件 = PosEventType：： BarcodeScannerTriggerPressed**                                                                             |
| UINT32                                 | **DataLength** = sizeof (**PosBarcodeScannerErrorOccurredData**) + **MessageLength**  +  **ScanDataLength**  +  **ScanDataLabelLength**)      |
| BOOL                                   | **IsRetriable**                                                                                                                         |
| 32位 UnifiedPosErrorSeverity         | **严重性**                                                                                                                            |
| UINT32                                 | **VendorErrorCode**                                                                                                                     |
| 32位 UnifiedPosErrorReason           | **原因**                                                                                                                              |
| UINT32                                 | **ExtendedReason**                                                                                                                      |
| UINT32                                 | **MessageLength**                                                                                                                       |
| PosBarcodeScannerDataReceivedEventData | **PartialData**                                                                                                                         |
| UINT32                                 | 未指定 **事件** 的                                                                                                             |
| UINT32                                 | **DataLength** = sizeof (**PosBarcodeScannerDataRecievedEventData**) + **MessageLength**  +  **ScanDataLength**  +  **ScanDataLabelLength**)  |
| UINT32                                 | 未指定 **数据类型**                                                                                                              |
| UINT32                                 | **ScanDataLength**                                                                                                                      |
| UINT32                                 | **ScanDataLabelLength**                                                                                                                 |
| 位 \[\]                              | **MessageLength** 字节的消息                                                                                                      |
| 位 \[\]                              | **ScanDataLength** 字节的标签数据                                                                                                  |
| 位 \[\]                              | 扫描数据的 **ScanDataLabelLength** 字节数                                                                                              |



## <a name="remarks"></a>备注

如果发生扫描错误，并且获取了某些扫描数据，则事件数据将包含部分扫描数据。

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface
