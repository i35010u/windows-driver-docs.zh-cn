---
title: EFI_USBFN_TRANSFER_STATUS
description: EFI_USBFN_TRANSFER_STATUS
ms.assetid: 60631dad-a617-4ed4-a975-5e480cf324e3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4aa9b795c851f1bc958bf05a5eef0bdae43a9c0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525702"
---
# <a name="efiusbfntransferstatus"></a>EFI\_USBFN\_传输\_状态


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
传输状态是未知的。

<a href="" id="usbtransferstatuscomplete"></a>**UsbTransferStatusComplete**  
传输已完成。

<a href="" id="usbtransferstatusaborted"></a>**UsbTransferStatusAborted**  
传输已中止。

<a href="" id="usbtransferstatusactive"></a>**UsbTransferStatusActive**  
传输处于活动状态。

<a href="" id="usbtransferstatusnone"></a>**UsbTransferStatusNone**  
传输具有无状态。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




