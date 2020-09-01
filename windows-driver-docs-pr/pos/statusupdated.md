---
title: StatusUpdated
description: 特定于设备的 StatusUpdated 事件表示电源更改通知等事件。
ms.assetid: e5d04e61-859a-49ee-bc54-58be4133b38a
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: ba3c6b6c5b885a6c0c52bfc09252940aa8e5819f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191915"
---
# <a name="statusupdated"></a>StatusUpdated

此特定于设备的事件表示电源更改通知等事件。

此事件的数据缓冲区如下所示。

## <a name="syntax"></a>语法

```cpp
typedef struct _PosStatusUpdatedEventData
{
    PosEventDataHeader Header;
    UINT32 Status;
    UINT32 ExtendedStatus;
} PosStatusUpdatedEventData;
```

下表显示此事件的数据缓冲区的内存布局。

| 内存值    | 说明 |
|-----------------| -------------------------------------------|
| 0x00000002 | **标头。事件 = PosEventType：： StatusUpdated**  |
| 0x00000010 | **DataLength** = Sizeof (**PosEventDataHeader**) + sizeof (**PosStatusUpdatedEventData** + sizeof (**PosStatusUpdatedEventData**)  |
| UINT32     | Status****。 请参阅 [BarcodeStatus](/windows-hardware/drivers/ddi/pointofservicecommontypes/ne-pointofservicecommontypes-_barcodestatus)。   |
| UINT32     | **ExtendedStatus** |

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface