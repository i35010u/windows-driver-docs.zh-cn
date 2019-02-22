---
title: EFI_USBFN_PORT_TYPE
description: EFI_USBFN_PORT_TYPE
ms.assetid: 2596dd4f-26bd-454b-9550-a89c7e1f790b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dea889b1b34bf22dcc97311dcb0693b54681e60f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543341"
---
# <a name="efiusbfnporttype"></a>EFI\_USBFN\_端口\_类型


此枚举指定 USB 端口类型。

## <a name="syntax"></a>语法


```cpp
typedef enum _EFI_USBFN_PORT_TYPE 
{
    EfiUsbUnknownPort = 0,
    EfiUsbStandardDownstreamPort,
    EfiUsbChargingDownstreamPort,
    EfiUsbDedicatedChargingPort,
    EfiUsbInvalidDedicatedChargingPort
} EFI_USBFN_PORT_TYPE;
```

## <a name="constants"></a>常量


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>EfiUsbUnknownPort</strong></p></td>
<td><p>未知端口-驱动程序内部的默认端口类型;这不会返回成功状态代码与驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><strong>EfiUsbStandardDownstreamPort</strong></p></td>
<td><p>标准 Downstream 端口-标准 USB host.for 的详细信息，请参阅<strong>备注</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EfiUsbChargingDownstreamPort</strong></p></td>
<td><p>充电 Downstream 端口-标准 USB 主机。 有关详细信息，请参阅<strong>备注</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>EfiUsbDedicatedChargingPort</strong></p></td>
<td><p>专用正在充电端口 – 墙充电器，非 USB 主机。 有关详细信息，请参阅<strong>备注</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>EfiUsbInvalidDedicatedChargingPort</strong></p></td>
<td><p>专用正在充电端口无效 – 不是 USB 主机或充电的专用的端口。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


请参阅"电池充电规范，修订版本 1.1"上的[USB.org](https://go.microsoft.com/fwlink/p/?linkid=64124)网站。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




