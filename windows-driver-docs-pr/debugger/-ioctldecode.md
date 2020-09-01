---
title: ioctldecode
description: Ioctldecode 扩展显示给定 IOCTL 代码指定的设备类型、所需访问权限、函数代码和传输类型。
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
ms.openlocfilehash: adac744f780505e513c2ae00b479a4cde4503c11
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217106"
---
# <a name="ioctldecode"></a>!ioctldecode


**！ Ioctldecode** extension 显示给定 IOCTL 代码指定的*设备类型*、*所需访问权限*、*函数代码*和*传输类型*。 有关 IOCTL 控制代码的详细信息，请参阅 [定义 I/o 控制代码](../kernel/defining-i-o-control-codes.md)。

```dbgcmd
!ioctldecode IoctlCode 
```

## <a name="span-idddk__ioresdes_dbgspanspan-idddk__ioresdes_dbgspanparameters"></a><span id="ddk__ioresdes_dbg"></span><span id="DDK__IORESDES_DBG"></span>参数


<span id="_______IoctlCode______"></span><span id="_______ioctlcode______"></span><span id="_______IOCTLCODE______"></span>*IoctlCode*   
指定十六进制 IOCTL 代码。 [**！ Irp**](-irp.md)命令在其输出中显示 IOCTL 代码。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

若要查看有关 IOCTL 的信息，我们首先找到相关的 IRP。 可以使用 [**！ irpfind**](-irpfind.md) 命令查找相关的 irp。

使用 [**！ irp**](-irp.md) 命令显示有关 irp 的信息。

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

显示的第三个参数（在本例中为 *0x220003*）是 IOCTL 代码。 使用 IOCTL 代码显示有关 IOCTL 的信息，在本例中为 [**ioctl \_ 内部 \_ USB \_ SUBMIT \_ URB**](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb)。

```dbgcmd
0: kd> !ioctldecode 0x220003

IOCTL_INTERNAL_USB_SUBMIT_URB

Device Type    : 0x22 (FILE_DEVICE_WINLOAD) (FILE_DEVICE_USER_MODE_BUS) (FILE_DEVICE_USB) (FILE_DEVICE_UNKNOWN)
Method         : 0x3 METHOD_NEITHER 
Access         : FILE_ANY_ACCESS
Function       : 0x0
```

如果提供的 IOCTL 代码不可用，则会看到这种类型的输出。

```dbgcmd
0: kd> !ioctldecode 0x1280ce

Unknown IOCTL  : 0x1280ce 

Device Type    : 0x12 (FILE_DEVICE_NETWORK)
Method         : 0x2 METHOD_OUT_DIRECT 
Access         : FILE_WRITE_ACCESS 
Function       : 0x33
```

尽管未标识 IOCTL，但会显示有关 IOCTL 字段的信息。

请注意，只有公共定义的 IOCTLs 的子集才能由 **！ ioctldecode** 命令标识。

有关 IOCTLs 的详细信息，请参阅 [I/o 控制代码简介](../kernel/introduction-to-i-o-control-codes.md)。

有关 Irp 和 IOCTLs 的更多常规信息，请参阅 *Windows 内部机制* ，方法为 Russinovich，David 为所罗门群岛和 Alex Ionescu。

 

