---
title: EFI_USBFN_IO_PROTOCOL.DetectPort
description: EFI_USBFN_IO_PROTOCOL.DetectPort
ms.assetid: 66f7500e-e075-495b-9ce0-aed2aa11f66a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 815b857212f225c7da8e9a87880d5333829a85ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337689"
---
# <a name="efiusbfnioprotocoldetectport"></a>EFI\_USBFN\_IO\_PROTOCOL.DetectPort


**DetectPort**函数返回的设备连接到 USB 端口类型。

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_DETECT_PORT) (
  IN EFI_USBFN_IO_PROTOCOL   *This,
  OUT EFI_USBFN_PORT_TYPE    *PortType
  );
```

## <a name="parameters"></a>Parameters


<a href="" id="this"></a>*此*  
指向 EFI\_USBFN\_IO\_协议实例。

<a href="" id="porttype"></a>*PortType*  
一个[EFI\_USBFN\_端口\_类型](efi-usbfn-port-type.md)枚举，指示 USB 端口类型。

## <a name="return-values"></a>返回值


此函数将返回以下值：

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
<td><p>成功返回的函数</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_INVALID_PARAMETER</strong></p></td>
<td><p>参数无效</p></td>
</tr>
<tr class="odd">
<td><p><strong>EFI_DEVICE_ERROR</strong></p></td>
<td><p>物理设备报告了错误。</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_NOT_READY</strong></p></td>
<td><p>物理设备是正忙还是未准备好处理此请求</p></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




