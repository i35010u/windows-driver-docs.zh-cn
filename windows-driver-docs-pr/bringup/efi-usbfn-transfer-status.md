---
title: EFI_USBFN_TRANSFER_STATUS
description: EFI_USBFN_TRANSFER_STATUS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a699e702d3b5c03e5065dd710408bf4444fefe30
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789003"
---
# <a name="efi_usbfn_transfer_status"></a>EFI \_ USBFN \_ 传输 \_ 状态


此枚举指示 USB 传输状态。

## <a name="syntax"></a>语法


```cpp
typedef enum _EFI_USBFN_TRANSFER_STATUS 
{
    UsbTransferStatusUnknown = 0,
    UsbTransferStatusComplete,
    UsbTransferStatusAborted,
    UsbTransferStatusActive,
    UsbTransferStatusNone
} EFI_USBFN_TRANSFER_STATUS;
```

## <a name="constants"></a>常量


<a href="" id="usbtransferstatusunknown"></a>**UsbTransferStatusUnknown**  
传输状态未知。

<a href="" id="usbtransferstatuscomplete"></a>**UsbTransferStatusComplete**  
传输完成。

<a href="" id="usbtransferstatusaborted"></a>**UsbTransferStatusAborted**  
已中止传输。

<a href="" id="usbtransferstatusactive"></a>**UsbTransferStatusActive**  
传输处于活动状态。

<a href="" id="usbtransferstatusnone"></a>**UsbTransferStatusNone**  
传输没有状态。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




