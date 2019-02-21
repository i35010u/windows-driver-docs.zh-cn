---
title: wudfext.umirps
description: Wudfext.umirps 扩展显示在主机进程的挂起用户模式下 I/O 请求数据包 (UM Irp) 的列表。
ms.assetid: bba78784-f4f5-432c-ad5e-837770de79d9
keywords:
- wudfext.umirps Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.umirps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 472d5d58584662ba19e9d2940c0f8e67da8ccc9e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541666"
---
# <a name="wudfextumirps"></a>!wudfext.umirps


**！ Wudfext.umirps**扩展插件都会显示在主机进程挂起用户模式下 I/O 请求数据包 (UM Irp) 的列表。

```dbgcmd
!wudfext.umirps NumberOfIrps Flags
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______NumberOfIrps______"></span><span id="_______numberofirps______"></span><span id="_______NUMBEROFIRPS______"></span> *NumberOfIrps*   
可选。 指定的挂起 UM Irp 以显示有关的信息的数目。 如果*NumberOfIrps*是一个星号 (\*) 或被省略，将显示所有 UM Irp 的所有 UM。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
可选。 指定要显示的信息的类型。 *标志*可以是以下位的任意组合。 默认值为 0x01。

<span id="Bit_0__0x01_"></span><span id="bit_0__0x01_"></span><span id="BIT_0__0X01_"></span>位 0 (0x01)  
显示有关挂起 Irp 的详细信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[用户模式驱动程序框架调试](user-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

挂起 UM 显示的 Irp 的列表可以提出向驱动程序或正在等待提供给该驱动程序。

默认情况下 **！ wudfext.umirps**显示所有 UM Irp。 但是，可以使用*NumberOfIrps*参数来限制此显示。

以下是一种 **！ wudfext.umirps**显示：

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

若要确定相应的内核模式 IRP，请使用[ **！ wudfext.wudfdownkmirp** ](-wudfext-wudfdownkmirp.md)扩展。 或者，可以使用中的值**UniqueId**并**KernelIrp**列与 UMDF IRP （或 UM IRP） 匹配到相应的内核 IRP。 可以将传递中的值**CWudfIrp**列与[ **！ wudfext.umirp** ](-wudfext-umirp.md)扩展，以确定框架**IWDFRequest**设备堆栈中的每个层可以访问的对象。

 

 





