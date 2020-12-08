---
title: EFI_USBFN_TRANSFER_RESULT
description: EFI_USBFN_TRANSFER_RESULT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e245668d0c3aacf476464ef06af11f30045620f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803355"
---
# <a name="efi_usbfn_transfer_result"></a>EFI \_ USBFN \_ 传输 \_ 结果


**EFI \_ USBFN \_ 传输 \_ 结果** 结构包含与主机传输或接收的数据有关的信息。

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


<a href="" id="bytestransferred"></a>**Microsoft.relay**  
传输的数据量（以字节为单位）。

<a href="" id="transferstatus"></a>**TransferStatus**  
类型为的 [EFI \_ USBFN \_ 传输 \_ 状态](efi-usbfn-transfer-status.md) 的枚举，用于指示传输状态。

<a href="" id="endpointindex"></a>**EndpointIndex**  
发生通知的终结点的索引。

<a href="" id="direction"></a>**方向键**  
终结点的方向。

<a href="" id="buffer"></a>**宽限**  
包含已传输数据的缓冲区。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




