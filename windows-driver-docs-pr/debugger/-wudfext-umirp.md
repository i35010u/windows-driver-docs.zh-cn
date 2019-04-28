---
title: wudfext.umirp
description: Wudfext.umirp 扩展显示有关主机的用户模式下 I/O 请求数据包 (UM IRP) 的信息。
ms.assetid: b31b864d-0c94-48b8-9ffd-f14639b9a551
keywords:
- wudfext.umirp Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.umirp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 62439be90140eecbfc96604b7bd8f91e22cac56e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347955"
---
# <a name="wudfextumirp"></a>!wudfext.umirp


**！ Wudfext.umirp**扩展显示有关主机的用户模式下 I/O 请求数据包 (UM IRP) 的信息。

```dbgcmd
!wudfext.umirp Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的地址 UM IRP 以显示有关的信息。

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

可以使用[ **！ wudfext.umirps** ](-wudfext-umirps.md)扩展命令以在主机进程显示所有未完成 UM Irp 的列表。

每个 UM IRP 具有一个或多个堆栈位置。 每个堆栈位置对应于设备堆栈中的单个驱动程序将接收调用以处理请求时的参数。

**！ wudfext.umirp**转储所有堆栈位置，并将标记当前位置与右尖括号 (&gt;)。 当前的位置对应于当前拥有该请求的驱动程序。 当前位置更改驱动程序将请求转发到下一步低驱动程序堆栈中或驱动程序完成驱动程序拥有的请求。

以下是一种 **！ wudfext.umirp**显示：

```dbgcmd
kd> !umirp 3dd480 
UM IRP: 0x003dd480  UniqueId: 0xde  Kernel Irp: 0x0x85377850
  Type: WudfMsg_READ
  ClientProcessId: 0x338
  Device Stack: 0x0034e4e0
  IoStatus
    hrStatus: 0x0
    Information: 0x0
  Driver/Framework created IRP: No
  Data Buffer: 0x00000000 / 0
  IsFrom32BitProcess: Yes
  CancelFlagSet: No
  Cancel callback: 0x01102224
  Total number of stack locations: 2
  CurrentStackLocation: 2 (StackLocation[ 1 ])
    StackLocation[ 0 ]
      UNINITIALIZED
  > StackLocation[ 1 ]
      IWDFRequest:  ????
      IWDFDevice:   0x000f2f80
      IWDFFile:     0x003a7648
      Completion:
        Callback:   0x00000000
        Context:    0x00000000
      Parameters: (RequestType: WdfRequestRead)
        Buffer length:        0x400
        Key:                  0x00000000
        Offset:               0x0
```

 

 





