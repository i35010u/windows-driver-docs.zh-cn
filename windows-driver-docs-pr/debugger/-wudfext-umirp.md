---
title: wudfext.umirp
description: Wudfext umirp 扩展显示有关主机用户模式 i/o 请求数据包 (UM IRP) 的信息。
keywords:
- wudfext umirp Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.umirp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e8ec6db92666993bcf4135339540ace63ef21e1a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794095"
---
# <a name="wudfextumirp"></a>!wudfext.umirp


**！ Wudfext umirp** 扩展显示有关主机用户模式 i/o 请求数据包 (UM IRP) 的信息。

```dbgcmd
!wudfext.umirp Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要显示其相关信息的 UM IRP 的地址。

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

你可以使用 [**！ wudfext umirps**](-wudfext-umirps.md) 扩展命令显示主机进程中所有未完成的 UM irp 的列表。

每个 UM IRP 都有一个或多个堆栈位置。 每个堆栈位置都对应于调用来处理请求时设备堆栈中的单个驱动程序将接收的参数。

**！ wudfext** 将转储所有堆栈位置，并使用右尖括号标记当前位置 (&gt;) 。 当前位置对应于当前拥有请求的驱动程序。 当驱动程序将请求转发到堆栈中的下一个较低的驱动程序时，或者当驱动程序完成驱动程序所拥有的请求时，当前位置将发生变化。

下面是 **！ wudfext** 显示的示例：

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

 

 





