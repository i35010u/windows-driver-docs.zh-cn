---
title: BarcodeScannerDataReceived
description: 成功扫描事件之后，BarcodeScannerDataReceived 事件发生。
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9933787164b175a8fabac6fef683db8dc1a6f1f2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794329"
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

| 内存值                                            | 描述                                                                                                                          |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| 0x00000005                                   | **标头。事件 = PosEventType：： BarcodeScannerDataReceived**                                                           |
| 0000020 + 扫描数据长度 + 标签数据长度 | **DataLength** = sizeof (**PosBarcodeScannerDataReceivedEventData**) + **ScanDataLength**  +  **ScanDataLabelLength** |
| UINT32                                       | **PosBarcodeScannerDataReceivedEventData**                                                                       |
| UINT32                                       | **PosBarcodeScannerDataReceivedEventData.ScanDataLength**                                                                 |
| UINT32                                       | **PosBarcodeScannerDataReceivedEventData.ScanDataLabelLength**                                                            |
| 位 \[\]                                    | 原始扫描数据的 **ScanDataLength** 字节数                                                                                 |
| 位 \[\]                                    | 解码扫描数据的 **ScanDataLabelLength** 字节数                                                                     |

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface
