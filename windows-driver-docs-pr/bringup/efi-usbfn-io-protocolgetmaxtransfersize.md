---
title: EFI_USBFN_IO_PROTOCOL.GetMaxTransferSize
description: EFI_USBFN_IO_PROTOCOL.GetMaxTransferSize
ms.assetid: 61160708-029b-4691-87fe-22d06424220d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e20d650747a0b14c572c5088c264e014d12e18f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337708"
---
# <a name="efiusbfnioprotocolgetmaxtransfersize"></a>EFI\_USBFN\_IO\_PROTOCOL.GetMaxTransferSize


**GetMaxTransferSize**函数返回的最大传输大小所支持的基础的控制器。

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_GET_MAXTRANSFER_SIZE) (
  IN EFI_USBFN_IO_PROTOCOL     *This,
  OUT UINTN                    *MaxTransferSize
  );
```

## <a name="parameters"></a>Parameters


<a href="" id="this"></a>*此*  
指向 EFI\_USBFN\_IO\_协议实例。

<a href="" id="maxtransfersize"></a>*MaxTransferSize*  
支持的最大传输大小，以字节为单位。

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

 

## <a name="remarks"></a>备注


## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




