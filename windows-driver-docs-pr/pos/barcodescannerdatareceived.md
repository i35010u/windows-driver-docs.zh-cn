---
title: BarcodeScannerDataReceived
description: 成功扫描事件之后，BarcodeScannerDataReceived 事件发生。
ms.assetid: 3dd7699a-5e2b-484b-bd83-c37ee7f0e851
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3efddbbc30476f896a9ad73c7f2d65c52f902573
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190425"
---
# <a name="barcodescannerdatareceived"></a>BarcodeScannerDataReceived

此事件在成功扫描事件之后发生。

扫描的数据为可变长度，并且包含 [PosBarcodeScannerDataReceivedEventData](/windows-hardware/drivers/ddi/pointofservicedriverinterface/ns-pointofservicedriverinterface-_posbarcodescannerdatareceivedeventdata) 结构，后跟 **ScanDataLength** 字节的原始扫描数据，后跟用于删除标头和表尾信息的解码扫描数据的 **ScanDataLabelLength** 字节，只保留扫描程序数据。 此事件的数据缓冲区如下所示。

## <a name="syntax"></a>语法

```cpp
typedef struct _PosBarcodeScannerDataReceivedEventData
{
    PosEventDataHeader Header;
    UINT32 DataType;
    UINT32 ScanDataLength;
    UINT32 ScanDataLabelLength;
} PosBarcodeScannerDataReceivedEventData;
```

下表显示此事件的数据缓冲区的内存布局。

| 内存值                                            | 说明                                                                                                                          |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| 0x00000005                                   | **标头。事件 = PosEventType：： BarcodeScannerDataReceived**                                                           |
| 0000020 + 扫描数据长度 + 标签数据长度 | **DataLength** = sizeof (**PosBarcodeScannerDataReceivedEventData**) + **ScanDataLength**  +  **ScanDataLabelLength** |
| UINT32                                       | **PosBarcodeScannerDataReceivedEventData**                                                                       |
| UINT32                                       | **PosBarcodeScannerDataReceivedEventData.ScanDataLength**                                                                 |
| UINT32                                       | **PosBarcodeScannerDataReceivedEventData.ScanDataLabelLength**                                                            |
| 位 \[\]                                    | 原始扫描数据的**ScanDataLength**字节数                                                                                 |
| 位 \[\]                                    | 解码扫描数据的**ScanDataLabelLength**字节数                                                                     |

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface