---
title: EFI_USBFN_IO_PROTOCOL.SetEndpointPolicy
description: EFI_USBFN_IO_PROTOCOL.SetEndpointPolicy
ms.assetid: d7ab0529-1925-47b5-9706-2e6288a6a5cf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1365e0454195d6476a69e430325e4212770abc56
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575404"
---
# <a name="efiusbfnioprotocolsetendpointpolicy"></a>EFI\_USBFN\_IO\_PROTOCOL.SetEndpointPolicy


**SetEndpointPolicy**函数设置指定非控制终结点的配置策略。

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_SET_ENDPOINT_POLICY) (
  IN EFI_USBFN_IO_PROTOCOL        *This,
  IN UINT8                        EndpointIndex,
  IN EFI_USBFN_ENDPOINT_DIRECTION Direction,
  IN EFI_USBFN_POLICY_TYPE        PolicyType,
  IN UINTN                        BufferSize,
  IN VOID                         *Buffer
  );
```

## <a name="parameters"></a>Parameters


<a href="" id="this"></a>*此*  
指向 EFI\_USBFN\_IO\_协议实例。

<a href="" id="endpointindex"></a>*EndpointIndex*  
指示策略需要设置非控制终结点。

<a href="" id="direction"></a>*方向*  
终结点的方向。 有关详细信息，请参阅[EFI\_USBFN\_终结点\_方向](efi-usbfn-endpoint-direction.md)。

<a href="" id="policytype"></a>*PolicyType*  
策略类型用户尝试设置指定非控制终结点。 有关详细信息，请参阅[EFI\_USBFN\_策略\_类型](efi-usbfn-policy-type.md)。

<a href="" id="buffersize"></a>*BufferSize*  
大小*缓冲区*以字节为单位。

<a href="" id="buffer"></a>*缓冲区*  
指向包含新的终结点策略值的缓冲区的指针。 策略类型的大小要求的详细信息，请参阅[EFI\_USBFN\_策略\_类型](efi-usbfn-policy-type.md)。

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
<td><p>该函数返回成功。</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_INVALID_PARAMETER</strong></p></td>
<td><p>参数无效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EFI_DEVICE_ERROR</strong></p></td>
<td><p>物理设备报告了错误。</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_UNSUPPORTED</strong></p></td>
<td><p>不支持更改此策略值。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


仅之前调用此函数[EFI\_USBFN\_IO\_协议。StartController](efi-usbfn-io-protocolstartcontroller.md)或之后[EFI\_USBFN\_IO\_协议。StopController](efi-usbfn-io-protocolstopcontroller.md)已调用。 此函数是可以开始于的修订 0x00010001 **EFI\_USBFN\_IO\_协议**。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




