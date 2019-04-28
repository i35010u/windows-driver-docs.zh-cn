---
title: EFI_USBFN_TRANSFER_RESULT
description: EFI_USBFN_TRANSFER_RESULT
ms.assetid: d101b061-2a83-4bf8-9502-ccb6e56f5cea
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0267bdc76cdd0cfeefc3bcdeb1b164686bdcfd3d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337692"
---
# <a name="efiusbfntransferresult"></a>EFI\_USBFN\_传输\_结果


**EFI\_USBFN\_传输\_结果**结构包含有关数据传输到或收到来自主机的信息。

## <a name="syntax"></a>语法


```cpp
typedef struct _EFI_USBFN_TRANSFER_RESULT 
{
    UINTN                         BytesTransferred;
    EFI_USBFN_TRANSFER_STATUS     TransferStatus;
    UINT8                         EndpointIndex;
    EFI_USBFN_ENDPOINT_DIRECTION  Direction;
    VOID                          *Buffer;
} EFI_USBFN_TRANSFER_RESULT;
```

## <a name="members"></a>成员


<a href="" id="bytestransferred"></a>**BytesTransferred**  
将传输的数据量，以字节为单位。

<a href="" id="transferstatus"></a>**TransferStatus**  
类型的枚举[EFI\_USBFN\_传输\_状态](efi-usbfn-transfer-status.md)，该值指示传输的状态。

<a href="" id="endpointindex"></a>**EndpointIndex**  
发生通知的终结点的索引。

<a href="" id="direction"></a>**方向**  
终结点的方向。

<a href="" id="buffer"></a>**缓冲区**  
包含传输的数据的缓冲区。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




