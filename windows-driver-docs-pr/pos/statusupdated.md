---
title: StatusUpdated
description: 特定于设备的 StatusUpdated 事件表示电源更改通知等事件。
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: a7a7351683842738241292f0c21c4a4dbd09abef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794301"
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

| 内存值    | 描述 |
|-----------------| -------------------------------------------|
| 0x00000002 | **标头。事件 = PosEventType：： StatusUpdated**  |
| 0x00000010 | **DataLength** = Sizeof (**PosEventDataHeader**) + sizeof (**PosStatusUpdatedEventData** + sizeof (**PosStatusUpdatedEventData**)  |
| UINT32     | Status。 请参阅 [BarcodeStatus](/windows-hardware/drivers/ddi/pointofservicecommontypes/ne-pointofservicecommontypes-_barcodestatus)。   |
| UINT32     | **ExtendedStatus** |

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface
