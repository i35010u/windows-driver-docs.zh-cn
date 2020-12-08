---
title: EFI_USBFN_POLICY_TYPE
description: EFI_USBFN_POLICY_TYPE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a36964f26dd4bad3013eade48f5296e7b40ae355
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803357"
---
# <a name="efi_usbfn_policy_type"></a>EFI \_ USBFN \_ 策略 \_ 类型


**EFI \_ USBFN \_ 策略 \_ 类型** 枚举包含用来指示终结点类型的值。

## <a name="syntax"></a>语法


```cpp
typedef enum _EFI_USBFN_POLICY_TYPE{
  EfiUsbPolicyUndefined = 0, 
  EfiUsbPolicyMaxTransactionSize, 
  EfiUsbPolicyZeroLengthTerminationSupport, 
  EfiUsbPolicyZeroLengthTermination
} EFI_USBFN_POLICY_TYPE;
```

## <a name="constants"></a>常量


<a href="" id="efiusbpolicyundefined"></a>**EfiUsbPolicyUndefined**  
不能跨驱动程序边界使用的策略值无效。 如果使用，则被调用方函数绝不能返回成功状态代码。

<a href="" id="efiusbpolicymaxtransactionsize"></a>**EfiUsbPolicyMaxTransactionSize**  
此策略为只读。 与 [EFI \_ USBFN \_ IO 协议一起使用时 \_ 。GetEndpointPolicy](efi-usbfn-io-protocolgetendpointpolicy.md)，将返回 (服务传递到) 控制器支持的终结点的最大单个事务大小。 它必须大于或等于可通过调用 [EFI \_ USBFN \_ IO 协议检索的最大传输大小 \_ 。GetMaxTransferSize](efi-usbfn-io-protocolgetmaxtransfersize.md)。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>GetEndpointPolicy</th>
<th>SetEndpointPolicy</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>BufferSize</em></p></td>
<td><p>4个字节，sizeof (UINT32) </p></td>
<td><p>不适用</p></td>
</tr>
<tr class="even">
<td><p>返回状态</p></td>
<td><p>EFI_STATUS</p></td>
<td><p>EFI_UNSUPPORTED</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="efiusbpolicyzerolengthterminationsupport"></a>**EfiUsbPolicyZeroLengthTerminationSupport**  
此策略为只读。 与 [EFI \_ USBFN \_ IO 协议一起使用时 \_ 。GetEndpointPolicy](efi-usbfn-io-protocolgetendpointpolicy.md)，如果 usb 控制器硬件能够在传输大小为 USB 最大数据包大小的倍数时自动处理长度为零的数据包，则返回 TRUE;如果控制器硬件不支持此类方案，则返回 FALSE。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>GetEndpointPolicy</th>
<th>SetEndpointPolicy</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>BufferSize</em></p></td>
<td><p>1个字节，sizeof (布尔) </p></td>
<td><p>不适用</p></td>
</tr>
<tr class="even">
<td><p>返回状态</p></td>
<td><p>EFI_STATUS</p></td>
<td><p>EFI_UNSUPPORTED</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="efiusbpolicyzerolengthtermination"></a>**EfiUsbPolicyZeroLengthTermination**  
与 [EFI \_ USBFN \_ IO 协议一起使用时 \_ 。GetEndpointPolicy](efi-usbfn-io-protocolgetendpointpolicy.md)，如果 usb 控制器硬件配置为在传输大小为 USB 最大数据包大小的倍数时自动处理长度为零的数据包，则返回 TRUE;如果控制器硬件未配置为支持这种情况，则返回 FALSE。

[EFI \_USBFN \_ IO \_ 协议。](efi-usbfn-io-protocolsetendpointpolicy.md) 如果 USB 控制器硬件能够支持自动零长度数据包终止，SetEndpointPolicy 只能接受此策略类型。 如果此值设置为 TRUE，则必须将控制器配置为处理指定终结点的零长度终止;如果值为 FALSE，则不会以这种方式配置控制器。

即使控制器硬件能够支持自动零长度终止，它也不能是默认配置。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>GetEndpointPolicy</th>
<th>SetEndpointPolicy</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>BufferSize</em></p></td>
<td><p>1个字节，sizeof (布尔) </p></td>
<td><p>1个字节，sizeof (布尔) </p></td>
</tr>
<tr class="even">
<td><p>返回状态</p></td>
<td><p>EFI_STATUS</p></td>
<td><p>EFI_STATUS</p></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




