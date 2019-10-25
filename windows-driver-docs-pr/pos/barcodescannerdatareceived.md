---
title: BarcodeScannerDataReceived
description: 成功扫描事件之后，BarcodeScannerDataReceived 事件发生。
ms.assetid: 3dd7699a-5e2b-484b-bd83-c37ee7f0e851
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: c6c1cff03e585c428ed8aac80aa0c038fcdce02b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843578"
---
# <a name="barcodescannerdatareceived"></a>BarcodeScannerDataReceived

此事件在成功扫描事件之后发生。

扫描的数据为可变长度，并且包含[PosBarcodeScannerDataReceivedEventData](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ns-pointofservicedriverinterface-_posbarcodescannerdatareceivedeventdata)结构，后跟**ScanDataLength**字节的原始扫描数据，后跟**ScanDataLabelLength**个字节的解码扫描数据，其中删除了页眉和页脚信息，只留下了扫描程序数据。 此事件的数据缓冲区如下所示。

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
| 0000020 + 扫描数据长度 + 标签数据长度 | **DataLength** = Sizeof （**PosBarcodeScannerDataReceivedEventData**） + **ScanDataLength** + **ScanDataLabelLength** |
| UINT32                                       | **PosBarcodeScannerDataReceivedEventData**                                                                       |
| UINT32                                       | **PosBarcodeScannerDataReceivedEventData.ScanDataLength**                                                                 |
| UINT32                                       | **PosBarcodeScannerDataReceivedEventData.ScanDataLabelLength**                                                            |
| 字节 \[\]                                    | 原始扫描数据的**ScanDataLength**字节数                                                                                 |
| 字节 \[\]                                    | 解码扫描数据的**ScanDataLabelLength**字节数                                                                     |

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface
