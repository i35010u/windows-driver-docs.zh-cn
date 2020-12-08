---
title: EFI_USBFN_IO_PROTOCOL.ConfigureEnableEndpointsEx
description: EFI_USBFN_IO_PROTOCOL.ConfigureEnableEndpointsEx
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a5a2924903020f3b5a8d3221001d3b5297a7b70
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803381"
---
# <a name="efi_usbfn_io_protocolconfigureenableendpointsex"></a>EFI \_ USBFN \_ IO \_PROTOCOL.ConfigureEnableEndpointsEx


基于提供的设备和配置描述符列表配置终结点。 类驱动程序可以在将 [EFI USBFN IO 替换为 \_ \_ \_ ureEnableEndpointsPROTOCOL.Config](efi-usbfn-io-protocolconfigureenableendpoints.md)的情况下调用此方法。

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
指向 EFI \_ USBFN \_ IO \_ 协议实例的指针。

<a href="" id="deviceinfo"></a>*DeviceInfo*  
指向 [EFI \_ USB \_ 设备 \_ 信息](efi-usb-device-info.md) 结构的指针。

<a href="" id="ssdeviceinfo"></a>*SSDeviceInfo*  
指向 [EFI \_ USB \_ SUPERSPEED \_ 设备 \_ 信息](efi-usb-superspeed-device-info.md) 结构的指针。

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


此函数可从 **EFI \_ USBFN \_ IO \_ 协议** 的修订版0x00010002 开始。

假设硬件已初始化，则此函数将使用提供的 *DeviceInfo* 配置终结点，激活端口并开始接收 USB 事件。 此函数接受 *DeviceInfo* 和 *SSDeviceInfo* 对象，并使用对象中的信息配置终结点，该对象支持基础硬件允许的最高速度。 传入的高速和超级速度 *DeviceInfo* 对象必须在 EFI \_ USB \_ 设备描述符中具有相同的 DeviceClass \_ 。 否则，此函数将返回 \_ 不受支持的 EFI。

此函数必须忽略标准终结点描述符的 *bMaxPacketSize0* *字段，该* 字段通过提供的 *DeviceInfo* 提供。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




