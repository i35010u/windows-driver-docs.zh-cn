---
title: EFI_USBFN_IO_PROTOCOL.ConfigureEnableEndpointsEx
description: EFI_USBFN_IO_PROTOCOL.ConfigureEnableEndpointsEx
ms.assetid: 54DE0D7F-788F-49C3-AF5C-7EDAA0D09D20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0ecd4fac8636e67f6e2e35b9b10071a658cd45c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547729"
---
# <a name="efiusbfnioprotocolconfigureenableendpointsex"></a>EFI\_USBFN\_IO\_PROTOCOL.ConfigureEnableEndpointsEx


配置基于提供的设备和配置描述符列表的终结点。 类驱动程序可能调用此方法中的替换[EFI\_USBFN\_IO\_协议。ConfigureEnableEndpoints](efi-usbfn-io-protocolconfigureenableendpoints.md)。

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_CONFIGURE_ENABLE_ENDPOINTS_EX) (
  IN EFI_USBFN_IO_PROTOCOL           *This,
  IN EFI_USB_DEVICE_INFO             *DeviceInfo,
  IN EFI_USB_SUPERSPEED_DEVICE_INFO  *SSDeviceInfo
  );
```

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
指向 EFI\_USBFN\_IO\_协议实例。

<a href="" id="deviceinfo"></a>*DeviceInfo*  
一个指向[EFI\_USB\_设备\_信息](efi-usb-device-info.md)结构。

<a href="" id="ssdeviceinfo"></a>*SSDeviceInfo*  
一个指向[EFI\_USB\_SUPERSPEED\_设备\_信息](efi-usb-superspeed-device-info.md)结构。

## <a name="return-values"></a>返回值


该函数返回以下值：

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
<td><p><strong>EFI_UNSUPPORTED</strong></p></td>
<td><p>不支持此操作。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


此函数是可以开始于的修订 0x00010002 **EFI\_USBFN\_IO\_协议**。

此函数假定硬件已初始化，将使用所提供的终结点配置*DeviceInfo*、 激活端口，并开始接收 USB 事件。 此函数可接受*DeviceInfo*并*SSDeviceInfo*对象，并配置的终结点支持的基础硬件所允许的最高速度的对象中的信息。 高速度和超级速度*DeviceInfo*中传递的对象必须在 EFI 中具有相同 DeviceClass\_USB\_设备\_描述符。 否则，此函数将返回 EFI\_不受支持。

此函数必须忽略*bMaxPacketSize0*标准设备描述符字段和*wMaxPacketSize*提供通过提供的标准终结点描述符字段*DeviceInfo*。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




