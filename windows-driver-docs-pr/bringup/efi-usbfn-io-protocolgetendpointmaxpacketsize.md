---
title: EFI_USBFN_IO_PROTOCOL.GetEndpointMaxPacketSize
description: EFI_USBFN_IO_PROTOCOL.GetEndpointMaxPacketSize
ms.assetid: 0af72372-7c58-490d-8eec-bd38bce09b0d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0571eb866c0566b0e82ca390fbfb9ba3b64aed7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337706"
---
# <a name="efiusbfnioprotocolgetendpointmaxpacketsize"></a>EFI\_USBFN\_IO\_PROTOCOL.GetEndpointMaxPacketSize


**GetEndpointMaxPacketSize**函数返回提供的总线速度的指定的终结点类型的最大数据包大小...

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_GET_ENDPOINT_MAXPACKET_SIZE) (
  IN EFI_USBFN_IO_PROTOCOL      *This,
  IN EFI_USB_ENDPOINT_TYPE      EndpointType,
  IN EFI_USB_BUS_SPEED          BusSpeed,
  OUT UINT16                    *MaxPacketSize
  );
```

## <a name="parameters"></a>Parameters


<a href="" id="this"></a>*此*  
指向 EFI\_USBFN\_IO\_协议实例。

<a href="" id="endpointtype"></a>*EndpointType*  
中定义的终结点类型[EFI\_USB\_终结点\_类型](efi-usb-endpoint-type.md)。 枚举

<a href="" id="busspeed"></a>*BusSpeed*  
[EFI\_USB\_总线\_速度](efi-usb-bus-speed.md)枚举值，该值指示当前的总线速度，因为调用方已知。

<a href="" id="maxpacketsize"></a>*MaxPacketSize*  
最大数据包大小，以字节为单位指定的终结点类型。

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

 

 




