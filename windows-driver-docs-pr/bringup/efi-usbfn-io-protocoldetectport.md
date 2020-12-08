---
title: EFI_USBFN_IO_PROTOCOL.DetectPort
description: EFI_USBFN_IO_PROTOCOL.DetectPort
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfe85ec74f49ae9a6fa5d71239eb910f8ed939e6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803377"
---
# <a name="efi_usbfn_io_protocoldetectport"></a>EFI \_ USBFN \_ IO \_ 协议。DetectPort


**DetectPort** 函数将返回连接到 USB 端口的设备的类型。

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_DETECT_PORT) (
  IN EFI_USBFN_IO_PROTOCOL   *This,
  OUT EFI_USBFN_PORT_TYPE    *PortType
  );
```

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
指向 EFI \_ USBFN \_ IO \_ 协议实例的指针。

<a href="" id="porttype"></a>*PortType*  
一个 [EFI \_ USBFN \_ 端口 \_ 类型](efi-usbfn-port-type.md) 枚举，用于指示 USB 端口类型。

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

 

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




