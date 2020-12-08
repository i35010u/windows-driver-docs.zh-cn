---
title: wudfext.umirps
description: Wudfext. umirps 扩展显示主机进程中 (UM Irp) 挂起的用户模式 i/o 请求包的列表。
keywords:
- wudfext umirps Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.umirps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d068249cb41e329eea4566306da798329309e1ad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794093"
---
# <a name="wudfextumirps"></a>!wudfext.umirps


**！ Wudfext umirps** 扩展显示主机进程中 (UM irp) 挂起的用户模式 i/o 请求包的列表。

```dbgcmd
!wudfext.umirps NumberOfIrps Flags
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______NumberOfIrps______"></span><span id="_______numberofirps______"></span><span id="_______NUMBEROFIRPS______"></span>*NumberOfIrps*   
可选。 指定要显示其相关信息的挂起的 UM Irp 的数目。 如果 *NumberOfIrps* 是星号 (\*) 或省略，则将显示所有 Um 的 um irp。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
可选。 指定要显示的信息的类型。 *标志* 可以是以下位的任意组合。 默认值为0x01。

<span id="Bit_0__0x01_"></span><span id="bit_0__0x01_"></span><span id="BIT_0__0X01_"></span>位 0 (0x01)   
显示有关挂起的 Irp 的详细信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Wudfext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [用户模式驱动程序框架调试](user-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

显示的挂起 UM Irp 的列表已显示给驱动程序，或者正在等待显示到驱动程序中。

默认情况下， **！ wudfext** 显示所有 UM irp。 但是，可以使用 *NumberOfIrps* 参数来限制此显示。

下面是 **！ wudfext** 显示的示例：

```dbgcmd
kd> !umirps 0xa 
Number of pending IRPS: 0xc8
####  CWudfIrp          Type        UniqueId          KernelIrp
----  ----------------  ----------  ----------------  ---------
0000            3dd280        READ                dc  856f02f0
0001            3dd380       WRITE                dd  85b869e0
0002            3dd480        READ                de  85377850
0003            3dd580        READ                df  93bba4e8
0004            3dd680       WRITE                e0  84cb9d70
0005            3dd780        READ                e1  85bec150
0006            3dd880       WRITE                e2  86651db0
0007            3dd980        READ                e3  85c22818
0008            3dda80        READ                e4  9961d150
0009            3ddb80       WRITE                e5  85c15148
```

若要确定相应的内核模式 IRP，请使用 [**！ wudfext**](-wudfext-wudfdownkmirp.md) 扩展名。 另外，还可以使用 **UniqueId** 和 **KernelIrp** 列中的值来匹配 UMDF IRP (或 UM irp) 到相应的内核 irp。 可以将 **CWudfIrp** 列中的值传递给 [**！ wudfext umirp**](-wudfext-umirp.md) 扩展，以确定设备堆栈中的每一层都可以访问的框架 **IWDFRequest** 对象。

 

 





