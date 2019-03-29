---
title: EFI_USBFN_IO_PROTOCOL.GetDeviceInfo
description: EFI_USBFN_IO_PROTOCOL.GetDeviceInfo
ms.assetid: b72f6ba1-7704-4661-8855-1ff88bd08e5a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92f35031fd4bec7d933003aef775c01f9d0ae061
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566638"
---
# <a name="efiusbfnioprotocolgetdeviceinfo"></a>EFI\_USBFN\_IO\_PROTOCOL.GetDeviceInfo


**GetDeviceInfo**函数将返回基于提供的标识符的特定于设备的信息

指定**EfiUsbDeviceInfoUnknown**如 Id 视为无效的参数。

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_GET_DEVICE_INFO) (
  IN EFI_USBFN_IO_PROTOCOL      *This,
  IN EFI_USBFN_DEVICE_INFO_ID   Id,
  IN OUT UINTN                  *BufferSize,
  OUT VOID                      *Buffer OPTIONAL
  );
```

## <a name="parameters"></a>Parameters


<a href="" id="this"></a>*此*  
指向 EFI\_USBFN\_IO\_协议实例。

<a href="" id="id"></a>*Id*  
一个[EFI\_USBFN\_设备\_信息\_ID](efi-usbfn-device-info-id.md)枚举，其中包含请求的设备 id。

<a href="" id="buffersize"></a>*BufferSize*  
在输入，以字节为单位的缓冲区的大小。 在输出时，数据量缓冲区中返回以字节为单位。

<a href="" id="buffer"></a>*缓冲区*  
指向所请求的信息将返回为 Unicode 字符串缓冲区的指针。

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
<td><p><strong>EFI_BUFFER_TOO_SMALL</strong></p></td>
<td><p>提供的缓冲区不够大以保存请求字符串。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


如果所提供的缓冲区太小或为 NULL，该方法将失败与**EFI\_缓冲区\_过\_小**和所需的大小通过返回**BufferSize**。 所有返回的字符串为 Unicode 格式。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




