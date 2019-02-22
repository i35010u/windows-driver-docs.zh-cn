---
title: ioctldecode
description: Ioctldecode 扩展显示为的给定 IOCTL 代码指定的设备类型、 所需的访问，函数代码和传输类型。
ms.assetid: 50B12034-E5C7-43F2-A31E-AAC824A05D46
keywords:
- ioctldecode Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ioctldecode
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2c1219778bf3f8b8ec125f52400c30e0003a5e27
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521457"
---
# <a name="ioctldecode"></a>!ioctldecode


**！ Ioctldecode**扩展显示*设备类型*，*所需访问*，*函数代码*和*传输类型*所指定的给定 IOCTL 代码。 IOCTL 控制代码的详细信息，请参阅[定义的 I/O 控制代码](https://msdn.microsoft.com/library/windows/hardware/ff543023)。

```dbgcmd
!ioctldecode IoctlCode 
```

## <a name="span-idddkioresdesdbgspanspan-idddkioresdesdbgspanparameters"></a><span id="ddk__ioresdes_dbg"></span><span id="DDK__IORESDES_DBG"></span>参数


<span id="_______IoctlCode______"></span><span id="_______ioctlcode______"></span><span id="_______IOCTLCODE______"></span> *IoctlCode*   
指定十六进制 IOCTL 代码。 [ **！ Irp** ](-irp.md)命令在其输出中显示的 IOCTL 代码。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

若要查看 IOCTL 的信息，我们首先找到感兴趣的 IRP。 可以使用[ **！ irpfind** ](-irpfind.md)命令来查找感兴趣的 irp。

使用[ **！ irp** ](-irp.md)命令以显示有关 irp 的信息。

```dbgcmd
0: kd> !irp ffffd581a6c6cd30
Irp is active with 6 stacks 6 is current (= 0xffffd581a6c6cf68)
No Mdl: No System Buffer: Thread 00000000:  Irp stack trace.  
     cmd  flg cl Device   File     Completion-Context
[N/A(0), N/A(0)]
            0  0 00000000 00000000 00000000-00000000    

                                                Args: 00000000 00000000 00000000 00000000
[N/A(0), N/A(0)]
            0  0 00000000 00000000 00000000-00000000    

                                                Args: 00000000 00000000 00000000 00000000
[N/A(0), N/A(0)]
            0  0 00000000 00000000 00000000-00000000    

                                                Args: 00000000 00000000 00000000 00000000
[N/A(0), N/A(0)]
            0  0 00000000 00000000 00000000-00000000    

                                                Args: 00000000 00000000 00000000 00000000
[N/A(0), N/A(0)]
            0  0 00000000 00000000 00000000-00000000    

                                                Args: 00000000 00000000 00000000 00000000
>[IRP_MJ_INTERNAL_DEVICE_CONTROL(f), N/A(0)]
            0 e1 ffffd581a5fbd050 00000000 fffff806d2412cf0-ffffd581a5cce050 Success Error Cancel pending
                       \Driver\usbehci        (IopUnloadSafeCompletion)
                                                Args: ffffd581a6c61a50 00000000 0x220003 00000000
```

在这种情况下显示的第三个参数*0x220003*，是 IOCTL 代码。 使用 IOCTL 代码来显示信息 IOCTL，在这种情况下[ **IOCTL\_内部\_USB\_提交\_URB**](https://msdn.microsoft.com/library/windows/hardware/ff537271)。

```dbgcmd
0: kd> !ioctldecode 0x220003

IOCTL_INTERNAL_USB_SUBMIT_URB

Device Type    : 0x22 (FILE_DEVICE_WINLOAD) (FILE_DEVICE_USER_MODE_BUS) (FILE_DEVICE_USB) (FILE_DEVICE_UNKNOWN)
Method         : 0x3 METHOD_NEITHER 
Access         : FILE_ANY_ACCESS
Function       : 0x0
```

如果您需要提供 IOCTL 代码不可用，您将看到此类型的输出。

```dbgcmd
0: kd> !ioctldecode 0x1280ce

Unknown IOCTL  : 0x1280ce 

Device Type    : 0x12 (FILE_DEVICE_NETWORK)
Method         : 0x2 METHOD_OUT_DIRECT 
Access         : FILE_WRITE_ACCESS 
Function       : 0x33
```

尽管无法识别 IOCTL，显示有关 IOCTL 字段的信息。

请注意，可以被识别的公开定义 Ioctl 一个子集 **！ ioctldecode**命令。

Ioctl 有关的详细信息请参阅[简介 I/O 控制代码](https://msdn.microsoft.com/library/windows/hardware/ff548059)。

有关 Irp 和 Ioctl 的更多常规信息，请参阅*Windows 内部结构*Mark E.Russinovich、 David A.Solomon 和 Alex Ionescu。

 

 





