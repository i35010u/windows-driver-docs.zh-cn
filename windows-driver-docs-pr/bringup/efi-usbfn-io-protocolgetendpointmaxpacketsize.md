---
title: EFI_USBFN_IO_PROTOCOL.GetEndpointMaxPacketSize
description: EFI_USBFN_IO_PROTOCOL.GetEndpointMaxPacketSize
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d454eb475012face06414009a4fb704f33a600ad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803371"
---
# <a name="efi_usbfn_io_protocolgetendpointmaxpacketsize"></a>EFI \_ USBFN \_ IO \_ 协议。GetEndpointMaxPacketSize


**GetEndpointMaxPacketSize** 函数为所提供的总线速度返回指定终结点类型的最大数据包大小。

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

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
指向 EFI \_ USBFN \_ IO \_ 协议实例的指针。

<a href="" id="endpointtype"></a>*EndpointType*  
在 [EFI \_ USB \_ 终结点 \_ 类型](efi-usb-endpoint-type.md)中定义的终结点类型。 枚举

<a href="" id="busspeed"></a>*BusSpeed*  
一个 [EFI \_ USB \_ 总线 \_ 速度](efi-usb-bus-speed.md) 枚举值，指示调用方已知的当前总线速度。

<a href="" id="maxpacketsize"></a>*MaxPacketSize*  
指定终结点类型的最大数据包大小（以字节为单位）。

## <a name="return-values"></a>返回值


此函数返回以下值：

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
<td><p>函数已成功返回</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_INVALID_PARAMETER</strong></p></td>
<td><p>参数无效</p></td>
</tr>
<tr class="odd">
<td><p><strong>EFI_DEVICE_ERROR</strong></p></td>
<td><p>物理设备报告了一个错误。</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_NOT_READY</strong></p></td>
<td><p>物理设备处于繁忙状态或尚未准备好处理此请求</p></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




