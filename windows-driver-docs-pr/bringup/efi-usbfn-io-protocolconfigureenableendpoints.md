---
title: EFI_USBFN_IO_PROTOCOL.ConfigureEnableEndpoints
description: EFI_USBFN_IO_PROTOCOL.ConfigureEnableEndpoints
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c17f697c9aa5648286a15b5e5d521846dd5d2238
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789035"
---
# <a name="efi_usbfn_io_protocolconfigureenableendpoints"></a>EFI \_ USBFN \_ IO \_PROTOCOL.ConfigureEnableEndpoints


**ConfigureEnableEndpoints** 函数基于提供的设备和配置描述符初始化终结点。

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_CONFIGURE_ENABLE_ENDPOINTS) (
  IN EFI_USBFN_IO_PROTOCOL         *This,
  IN EFI_USB_DEVICE_INFO           *DeviceInfo
  );
```

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
指向 EFI \_ USBFN \_ IO \_ 协议实例的指针。

<a href="" id="deviceinfo"></a>*DeviceInfo*  
指向 [EFI \_ USB \_ 设备 \_ 信息](efi-usb-device-info.md) 结构的指针。

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
<tr class="odd">
<td><p><strong>EFI_OUT_OF_RESOURCES</strong></p></td>
<td><p>由于缺少资源，无法完成请求。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


假设硬件已初始化，则此函数将使用提供的 *DeviceInfo* 配置终结点，激活端口并开始接收 USB 事件。

此函数必须忽略标准终结点描述符的 *bMaxPacketSize0* *字段，该* 字段通过提供的 *DeviceInfo* 提供。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




