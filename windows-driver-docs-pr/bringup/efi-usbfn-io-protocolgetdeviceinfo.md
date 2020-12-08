---
title: EFI_USBFN_IO_PROTOCOL.GetDeviceInfo
description: EFI_USBFN_IO_PROTOCOL.GetDeviceInfo
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 013f6d6c1cacad7bba20eeb7423868c9f16c968d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803373"
---
# <a name="efi_usbfn_io_protocolgetdeviceinfo"></a>EFI \_ USBFN \_ IO \_ 协议。GetDeviceInfo


**GetDeviceInfo** 函数基于提供的标识符返回特定于设备的信息

将 **EfiUsbDeviceInfoUnknown** 指定为 Id 会被视为无效的参数。

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

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
指向 EFI \_ USBFN \_ IO \_ 协议实例的指针。

<a href="" id="id"></a>*识别*  
一个 [EFI \_ USBFN \_ 设备 \_ 信息 \_ id](efi-usbfn-device-info-id.md) 枚举，其中包含请求的设备 id。

<a href="" id="buffersize"></a>*BufferSize*  
输入时，缓冲区的大小（以字节为单位）。 输出时，以字节为单位返回的数据量。

<a href="" id="buffer"></a>*宽限*  
指向缓冲区的指针，请求的信息将作为 Unicode 字符串返回。

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
<td><p><strong>EFI_BUFFER_TOO_SMALL</strong></p></td>
<td><p>提供的缓冲区不够大，无法容纳请求字符串。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


如果所提供的缓冲区太小或为 NULL，则该方法将失败，并且 **EFI \_ 缓冲区 \_ 太 \_ 小** ，并通过 **BufferSize** 返回所需大小。 所有返回的字符串都是 Unicode 格式。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




