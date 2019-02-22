---
title: EFI_USBFN_POLICY_TYPE
description: EFI_USBFN_POLICY_TYPE
ms.assetid: 51f615d4-a226-45d5-b5e9-fea4859640a9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fba94c165161fe8a6131cd74ed5402d5e322552
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555868"
---
# <a name="efiusbfnpolicytype"></a>EFI\_USBFN\_策略\_类型


**EFI\_USBFN\_策略\_类型**枚举包含用来指示终结点的类型的值。

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
无效的策略必须永远不会使用跨驱动程序边界的值。 如果使用，被调用方函数必须永远不会返回成功状态代码。

<a href="" id="efiusbpolicymaxtransactionsize"></a>**EfiUsbPolicyMaxTransactionSize**  
此策略是只读的。 与一起使用时[EFI\_USBFN\_IO\_协议。GetEndpointPolicy](efi-usbfn-io-protocolgetendpointpolicy.md)，返回由控制器支持的最大的单个事务 （交付服务的终结点） 的大小。 它必须是详细或等于最大传输大小，可以通过调用来检索[EFI\_USBFN\_IO\_协议。GetMaxTransferSize](efi-usbfn-io-protocolgetmaxtransfersize.md)。

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
<td><p>4 bytes, sizeof(UINT32)</p></td>
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
此策略是只读的。 与一起使用时[EFI\_USBFN\_IO\_协议。GetEndpointPolicy](efi-usbfn-io-protocolgetendpointpolicy.md)，如果 USB 控制器硬件能够支持的传输大小的倍数 USB 最大数据包大小; 时自动处理零长度的数据包，则返回 TRUE如果控制器硬件不支持此类方案，则返回 FALSE。

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
<td><p>1 个字节、 sizeof(BOOLEAN)</p></td>
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
与一起使用时[EFI\_USBFN\_IO\_协议。GetEndpointPolicy](efi-usbfn-io-protocolgetendpointpolicy.md)，如果 USB 控制器硬件配置为自动处理零长度的数据包的传输大小是 USB 最大数据包大小; 的倍数时，则返回 TRUE如果控制器硬件未配置为支持这种方案，则返回 FALSE。

[EFI\_USBFN\_IO\_协议。SetEndpointPolicy](efi-usbfn-io-protocolsetendpointpolicy.md) USB 控制器硬件能够支持自动长度为零的数据包终止是否只能接受此策略类型。 当此值设置为 TRUE 时，必须配置控制器来处理指定的终结点; 的长度为零终止FALSE 值不会以这种方式配置控制器。

即使控制器硬件能够支持自动长度为零终止，它必须不是默认配置。

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
<td><p>1 个字节、 sizeof(BOOLEAN)</p></td>
<td><p>1 个字节、 sizeof(BOOLEAN)</p></td>
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

 

 




