---
title: ks. objhdr
description: Objhdr 扩展显示与指定文件对象关联的内核流式处理对象标头。
keywords:
- objhdr Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.objhdr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7e253fd6fe1e503628c51a20b9899c447316e2cf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792435"
---
# <a name="ksobjhdr"></a>!ks.objhdr


**Objhdr** 扩展显示与指定文件对象关联的内核流式处理对象标头。

```dbgcmd
!ks.objhdr FileObject [Level] [Flags]  
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______FileObject______"></span><span id="_______fileobject______"></span><span id="_______FILEOBJECT______"></span>*FileObject*   
此参数指定指向 WDM 文件对象的指针。 如果 *FileObject* 无效，则该命令将返回错误。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span>*级别*   
可选。 值与 [**！ ks**](-ks-dump.md)的值相同。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
可选。 值与 [**！ ks**](-ks-dump.md)的值相同。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>winxp\Ks.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ks.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核流调试](kernel-streaming-debugging.md)。

<a name="remarks"></a>备注
-------

**！ Ks** 的级别和标志与 [**！ ks**](-ks-dump.md)中描述的 objhdr 相同。

从！ ks. [**allstreams**](-ks-allstreams.md) 和 [**！ enumdevobj**](-ks-enumdevobj.md) 的输出可以用作 **！ objhdr** 的输入。 例如，若要通过 *avssamp* 示例执行此操作，请发出以下命令：

```dbgcmd
kd> !ks.allstreams
6 Kernel Streaming FDOs found:
    Functional Device 8299be18 [\Driver\smwdm]
    Functional Device 827c86d8 [\Driver\wdmaud]
    Functional Device 827c0f08 [\Driver\sysaudio]
    Functional Device 82424590 [\Driver\avssamp]
    Functional Device 82423720 [\Driver\MSPQM]
    Functional Device 82b91a88 [\Driver\MSPCLOCK]
kd> !ks.enumdevobj 82424590
WDM device object 82424590:
    Corresponding KSDEVICE        82427540
    Factory 8285baa4 [Descriptor f7a333c8] instances:
        82837a34 
kd> !ks.objhdr 82837a34 7
```

此命令的结果可能很长。 发出 Ctrl BREAK (WinDbg) 或 Ctrl-c (NTSD、CDB、KD) 停止输出。

下面是一个单独的示例：

```dbgcmd
kd> !ks.objhdr 81D828B8 7
Adjusting file object 81D828B8 to object header 81BC1008

Object Header 81BC1008
    Associated Create Items:
        Create Item F9F77E98
            CreateFunction = ks!CKsFilter::DispatchCreatePin+0x00
            ObjectClass = {146F1A80-4791-11D0-A5D6-28DB04C10000}
            Flags = 0
    Child Create Handler List:
        Create Item F9F85AA0
            CreateFunction = ks!CKsPin::DispatchCreateAllocator+0x00
            ObjectClass = {642F5D00-4791-11D0-A5D6-28DB04C10000}
            Flags = 0
        Create Item F9F85AB8
            CreateFunction = ks!CKsPin::DispatchCreateClock+0x00
            ObjectClass = {53172480-4791-11D0-A5D6-28DB04C10000}
            Flags = 0
        Create Item F9F85AD0
            CreateFunction = ks!CKsPin::DispatchCreateNode+0x00
            ObjectClass = {0621061A-EE75-11D0-B915-00A0C9223196}
            Flags = 0
    DispatchTable:
        Dispatch Table F9F85AE8
            DeviceIoControl = ks!CKsPin::DispatchDeviceIoControl+0x00
            Read = ks!KsDispatchInvalidDeviceRequest+0x00
            Write = ks!KsDispatchInvalidDeviceRequest+0x00
            Flush = ks!KsDispatchInvalidDeviceRequest+0x00
            Close = ks!CKsPin::DispatchClose+0x00
            QuerySecurity = ks!KsDispatchQuerySecurity+0x00
            SetSecurity = ks!KsDispatchSetSecurity+0x00
            FastDeviceIoControl = ks!KsDispatchFastIoDeviceControlFailure+0x00
            FastRead = ks!KsDispatchFastReadFailure+0x00
            FastWrite = ks!KsDispatchFastReadFailure+0x00
    TargetState: KSTARGET_STATE_ENABLED
    TargetDevice: 00000000
    BaseDevice  : 81BBDF10
    Stack Depth : 1
    Corresponding AVStream object = 81A971B0
```

 

 





