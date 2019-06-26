---
title: StatusUpdated
description: 特定于设备的 StatusUpdated 事件表示事件，如电源更改通知。
ms.assetid: e5d04e61-859a-49ee-bc54-58be4133b38a
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: c1cdd2759b564f54f27790095bc67a60e33997a3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386500"
---
# <a name="statusupdated"></a>StatusUpdated

此特定于设备的事件表示事件，如电源更改通知。

此事件的数据缓冲区是按如下所示。

## <a name="syntax"></a>语法

```cpp
typedef struct _PosStatusUpdatedEventData
{
    PosEventDataHeader Header;
    UINT32 Status;
    UINT32 ExtendedStatus;
} PosStatusUpdatedEventData;
```

下表显示了此事件的数据缓冲区的内存布局。

| 内存值    | 描述 |
|-----------------| -------------------------------------------|
| 0x00000002 | **Header.EventType = PosEventType::StatusUpdated**  |
| 0x00000010 | **Header.DataLength** = sizeof(**PosEventDataHeader**) + sizeof(**PosStatusUpdatedEventData.Status** + sizeof(**PosStatusUpdatedEventData.ExtendedStatus**) |
| UINT32     | **状态**。 请参阅[BarcodeStatus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicecommontypes/ne-pointofservicecommontypes-_barcodestatus)。   |
| UINT32     | **ExtendedStatus** |

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface.h
