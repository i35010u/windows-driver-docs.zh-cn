---
title: EFI_USBFN_IO_PROTOCOL.SetEndpointPolicy
description: EFI_USBFN_IO_PROTOCOL.SetEndpointPolicy
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 467e9115c47cee1a051084ae874a2baeda5d884a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789025"
---
# <a name="efi_usbfn_io_protocolsetendpointpolicy"></a>EFI \_ USBFN \_ IO \_ 协议。SetEndpointPolicy


**SetEndpointPolicy** 函数为指定的非控制终结点设置配置策略。

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

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
指向 EFI \_ USBFN \_ IO \_ 协议实例的指针。

<a href="" id="endpointindex"></a>*EndpointIndex*  
指示需要为其设置策略的非控制终结点。

<a href="" id="direction"></a>*方向键*  
终结点的方向。 有关详细信息，请参阅 [EFI \_ USBFN \_ 终结点 \_ 方向](efi-usbfn-endpoint-direction.md)。

<a href="" id="policytype"></a>*PolicyType*  
用户试图为指定的非控制终结点设置的策略类型。 有关详细信息，请参阅 [EFI \_ USBFN \_ 策略 \_ 类型](efi-usbfn-policy-type.md)。

<a href="" id="buffersize"></a>*BufferSize*  
*缓冲区* 的大小（以字节为单位）。

<a href="" id="buffer"></a>*宽限*  
指向包含新终结点策略值的缓冲区的指针。 有关策略类型的大小要求的详细信息，请参阅 [EFI \_ USBFN \_ 策略 \_ 类型](efi-usbfn-policy-type.md)。

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
<td><p>函数已成功返回。</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_INVALID_PARAMETER</strong></p></td>
<td><p>参数无效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EFI_DEVICE_ERROR</strong></p></td>
<td><p>物理设备报告了一个错误。</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_UNSUPPORTED</strong></p></td>
<td><p>不支持更改此策略值。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


只能在 [EFI \_ USBFN \_ IO 协议之前调用此函数 \_ 。StartController](efi-usbfn-io-protocolstartcontroller.md) 或 [EFI \_ USBFN \_ IO 协议后 \_ 。](efi-usbfn-io-protocolstopcontroller.md) 已调用 StopController。 此函数可从 **EFI \_ USBFN \_ IO \_ 协议** 的修订版0x00010001 开始。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




