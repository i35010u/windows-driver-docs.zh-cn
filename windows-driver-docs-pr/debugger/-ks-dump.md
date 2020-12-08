---
title: ks. 转储
description: Ks 扩展显示指定的对象。
keywords:
- ks. 转储 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.dump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a86d00f9876da5f69afec108b552df5aeb794d8a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826739"
---
# <a name="ksdump"></a>!ks.dump


**！ Ks** 扩展显示指定的对象。

```dbgcmd
!ks.dump Object [Level] [Flags]  
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span>*对象*   
指定指向 AVStream 结构的指针、AVStream 类对象或 PortCls 对象。 还可以指定指向 IRP 或文件对象的指针。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span>*级别*   
可选。 指定要在0-7 刻度上显示的详细信息的级别，并为较高的值显示更多的信息。 若要显示所有可用的详细信息，请提供值7。 可以通过发出不带参数的 **！ ks** 命令来查看有关级别的详细信息。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
可选。 指定要显示的信息的类型。 *标志* 可以是以下位的任意组合。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
显示所有排队的 Irp。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)   
显示所有挂起的 Irp。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)   
分析被怀疑的关系图。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>第 3 (0x8)   
显示所有 pin 状态。

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

**！ Ks** 命令识别大多数 AVStream 对象，其中包括 pin、筛选器、工厂、设备、管道和流指针。 此命令还识别一些 stream 类结构，包括流对象、筛选器实例、设备扩展和 SRBs。

下面是用于筛选器的 **！ ks** 显示示例的示例：

```dbgcmd
kd> !dump 829493c4
Filter object 829493c4 [CKsFilter = 82949350]
    Descriptor     f7a233c8:
    Context        829dce28
```

下面是一个 pin 的 **！ ks** 示例显示示例：

```dbgcmd
kd> !dump 8160DDE0 7
Pin object 8160DDE0 [CKsPin = 8160DD50]
    DeviceState    KSSTATE_RUN
    ClientState    KSSTATE_RUN
    ResetState     KSRESET_END
    CKsPin object 8160DD50 [KSPIN = 8160DDE0]
        State                    KSSTATE_RUN
        Processing Mutex         8160DFD0 is not held
        And Gate &               8160DF88
        And Gate Count           1
```

下表中提供了此显示的一些重要部分。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>参数</strong></p></td>
<td align="left"><p><strong>含义</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>DeviceState</p></td>
<td align="left"><p>请求输入的 pin 状态。 如果不同于 ClientState，则这是微型驱动程序将转换到下一步的状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ClientState</p></td>
<td align="left"><p>微型驱动程序实际处于的状态。 这反映了管道的状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ResetState</p></td>
<td align="left"><p>指示对象是否处于刷新中间。</p>
<p>KSRESET_BEGIN 指示刷新。</p>
<p>KSRESET_END 指示不刷新。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>状态</p></td>
<td align="left"><p>Pin 传输到非 AVStream 筛选器的内部状态。</p></td>
</tr>
</tbody>
</table>

 

下面是一个针对 stream 类驱动程序的 **！ ks** 显示示例的示例：

```dbgcmd
kd> !dump 81a0a170 7
Device Extension 81a0a228:
    Device Object          81a0a170 [\Driver\TESTCAP]
    Next Device Object     81bd56d8 [\Driver\PnpManager]
    Physical Device Object 81bd56d8 [\Driver\PnpManager]
    REGISTRY FLAGS:
        Page out driver when closed
        No suspend if running
    MINIDRIVER Data:
        Device Extension       81a0a44c
        Interrupt Routine      00000000
        Synchronize Routine    STREAM!StreamClassSynchronizeExecution
        Receive Device SRB     testcap!AdapterReceivePacket
        Cancel Packet          testcap!AdapterCancelPacket
        Timeout Packet         testcap!AdapterTimeoutPacket
        Size (d / r / s / f)   1a0(416), 14(20), 978(2424), 0(0)
        Sync Mode              Driver Synchronizes
    Filter Type 0:
        Symbolic Links:
            Information Paged Out
        Instances:
            816b7bd8
```

请注意，大小以十六进制数列出，然后在十进制等效的本次中列出。 下表列出了此显示屏中的大小缩写。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>大小</strong></p></td>
<td align="left"><p><strong>解释</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>d</p></td>
<td align="left"><p>设备</p></td>
</tr>
<tr class="odd">
<td align="left"><p>r</p></td>
<td align="left"><p>请求</p></td>
</tr>
<tr class="even">
<td align="left"><p>s</p></td>
<td align="left"><p>Stream</p></td>
</tr>
<tr class="odd">
<td align="left"><p>F</p></td>
<td align="left"><p>筛选器. 如果筛选器大小为0，则筛选器为单实例。 如果大于0，则为多实例。</p></td>
</tr>
</tbody>
</table>

 

 

 





