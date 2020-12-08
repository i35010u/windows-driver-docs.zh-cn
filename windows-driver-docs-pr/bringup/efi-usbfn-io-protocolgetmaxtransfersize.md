---
title: EFI_USBFN_IO_PROTOCOL.GetMaxTransferSize
description: EFI_USBFN_IO_PROTOCOL.GetMaxTransferSize
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7efb954da7f17742fa62960516b8993c1e875b43
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789033"
---
# <a name="efi_usbfn_io_protocolgetmaxtransfersize"></a>EFI \_ USBFN \_ IO \_ 协议。GetMaxTransferSize


**GetMaxTransferSize** 函数将返回基础控制器支持的最大传输大小。

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_GET_MAXTRANSFER_SIZE) (
  IN EFI_USBFN_IO_PROTOCOL     *This,
  OUT UINTN                    *MaxTransferSize
  );
```

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
指向 EFI \_ USBFN \_ IO \_ 协议实例的指针。

<a href="" id="maxtransfersize"></a>*MaxTransferSize*  
支持的最大传输大小（以字节为单位）。

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

 

## <a name="remarks"></a>备注


## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




