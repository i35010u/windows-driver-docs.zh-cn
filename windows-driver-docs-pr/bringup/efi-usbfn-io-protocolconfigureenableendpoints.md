---
title: EFI_USBFN_IO_PROTOCOL.ConfigureEnableEndpoints
description: EFI_USBFN_IO_PROTOCOL.ConfigureEnableEndpoints
ms.assetid: 31bc58a0-ec2b-4b5e-ad1b-e6107cc083b1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09a3678c88ad507b5e9fbd03533e923beb3f38fe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568157"
---
# <a name="efiusbfnioprotocolconfigureenableendpoints"></a>EFI\_USBFN\_IO\_PROTOCOL.ConfigureEnableEndpoints


**ConfigureEnableEndpoints**函数初始化的终结点提供的设备和配置描述符。

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_CONFIGURE_ENABLE_ENDPOINTS) (
  IN EFI_USBFN_IO_PROTOCOL         *This,
  IN EFI_USB_DEVICE_INFO           *DeviceInfo
  );
```

## <a name="parameters"></a>Parameters


<a href="" id="this"></a>*此*  
指向 EFI\_USBFN\_IO\_协议实例。

<a href="" id="deviceinfo"></a>*DeviceInfo*  
一个指向[EFI\_USB\_设备\_信息](efi-usb-device-info.md)结构。

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
<tr class="odd">
<td><p><strong>EFI_OUT_OF_RESOURCES</strong></p></td>
<td><p>缺少资源，无法完成由于请求。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


此函数假定硬件已初始化，将使用所提供的终结点配置*DeviceInfo* 、 激活端口，并开始接收 USB 事件。

此函数必须忽略*bMaxPacketSize0*标准设备描述符字段和*wMaxPacketSize*提供通过提供的标准终结点描述符字段*DeviceInfo*。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




