---
title: StatusUpdated
description: 特定于设备的 StatusUpdated 事件表示电源更改通知等事件。
ms.assetid: e5d04e61-859a-49ee-bc54-58be4133b38a
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2107c3b30ec46a6ca3a07cbb63f81deeba0464a8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841643"
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
| 0x00000010 | **DataLength** = Sizeof （**PosEventDataHeader**） + sizeof （**PosStatusUpdatedEventData** + sizeof （**PosStatusUpdatedEventData**） |
| UINT32     | **状态**。 请参阅[BarcodeStatus](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicecommontypes/ne-pointofservicecommontypes-_barcodestatus)。   |
| UINT32     | **ExtendedStatus** |

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface
