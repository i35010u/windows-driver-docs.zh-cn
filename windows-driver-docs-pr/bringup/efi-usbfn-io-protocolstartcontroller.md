---
title: EFI_USBFN_IO_PROTOCOL.StartController
description: EFI_USBFN_IO_PROTOCOL.StartController
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef8cce7f5b0eee872a1ce0706cef0abb4fb5b5b4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789029"
---
# <a name="efi_usbfn_io_protocolstartcontroller"></a>EFI \_ USBFN \_ IO \_ 协议。StartController


如果需要， **StartController** 函数提供 USB 控制器的电源，并初始化硬件和内部数据结构。 此函数不得激活该端口。

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_START_CONTROLLER) (
  IN EFI_USBFN_IO_PROTOCOL        *This
  );
```

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
指向 EFI \_ USBFN \_ IO \_ 协议实例的指针。

## <a name="return-values"></a>返回值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>返回代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>EFI_SUCCESS</strong></p></td>
<td><p>函数已成功返回。</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_INVALID_PARAMETER</strong></p></td>
<td><p>参数无效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EFI_DEVICE_ERROR</strong></p></td>
<td><p>物理设备报告了一个错误。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


此函数可从 **EFI \_ USBFN \_ IO \_ 协议** 的修订版0x00010001 开始。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




