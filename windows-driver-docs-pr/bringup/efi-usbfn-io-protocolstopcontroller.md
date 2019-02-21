---
title: EFI_USBFN_IO_PROTOCOL.StopController
description: EFI_USBFN_IO_PROTOCOL.StopController
ms.assetid: 531fd280-bcb1-4b6f-a2fa-9052318171b3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 366b30016650084b171e94321117fae20d6eab0d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532976"
---
# <a name="efiusbfnioprotocolstopcontroller"></a>EFI\_USBFN\_IO\_PROTOCOL.StopController


**StopController**函数通过重置运行/停止位和关闭 USB 控制器，如有必要禁用硬件设备。

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_STOP_CONTROLLER) (
  IN EFI_USBFN_IO_PROTOCOL        *This
  );
```

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
指向 EFI\_USBFN\_IO\_协议实例。

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
<td><p>该函数返回成功。</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_INVALID_PARAMETER</strong></p></td>
<td><p>参数无效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EFI_DEVICE_ERROR</strong></p></td>
<td><p>物理设备报告了错误。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


此函数是可以开始于的修订 0x00010001 **EFI\_USBFN\_IO\_协议**。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




