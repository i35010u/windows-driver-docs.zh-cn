---
title: BarcodeScannerDataReceived
description: 成功扫描事件之后发生 BarcodeScannerDataReceived 事件。
ms.assetid: 3dd7699a-5e2b-484b-bd83-c37ee7f0e851
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4d163fb0b0f679d71dc8f5692dd8bd8e8af62f83
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544000"
---
# <a name="barcodescannerdatareceived"></a>BarcodeScannerDataReceived

成功扫描事件之后发生此事件。

扫描的数据是可变长度，组成[PosBarcodeScannerDataReceivedEventData](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicedriverinterface/ns-pointofservicedriverinterface-_posbarcodescannerdatareceivedeventdata
)结构跟**ScanDataLength**字节的原始扫描数据后跟**ScanDataLabelLength**解码的扫描数据在其中删除页眉和页脚信息，它仅将扫描程序数据保留的字节。 此事件的数据缓冲区是按如下所示。

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

下表显示了此事件的数据缓冲区的内存布局。

| 内存值                                            | 描述                                                                                                                          |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| 0x00000005                                   | **Header.EventType = PosEventType::BarcodeScannerDataReceived**                                                           |
| 0000020 + 扫描数据长度 + 标签数据长度 | **Header.DataLength** = sizeof(**PosBarcodeScannerDataReceivedEventData**) + **ScanDataLength** + **ScanDataLabelLength** |
| UINT32                                       | **PosBarcodeScannerDataReceivedEventData.DataType**                                                                       |
| UINT32                                       | **PosBarcodeScannerDataReceivedEventData.ScanDataLength**                                                                 |
| UINT32                                       | **PosBarcodeScannerDataReceivedEventData.ScanDataLabelLength**                                                            |
| byte \[\]                                    | **ScanDataLength**的原始扫描数据的字节                                                                                 |
| byte \[\]                                    | **ScanDataLabelLength**解码的扫描数据的字节                                                                     |

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface.h
