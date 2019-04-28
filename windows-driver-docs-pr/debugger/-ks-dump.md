---
title: ks.dump
description: Ks.dump 扩展显示指定的对象。
ms.assetid: 7878c79f-9de6-4fd2-9641-c636212429eb
keywords:
- ks.dump Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.dump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 81b6db8685a6b6841febcbec68379362a2eab817
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336661"
---
# <a name="ksdump"></a>!ks.dump


**！ Ks.dump**扩展显示指定的对象。

```dbgcmd
!ks.dump Object [Level] [Flags]  
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span> *Object*   
指定指向 AVStream 结构、 AVStream 类对象或 PortCls 对象的指针。 此外可以指定 IRP 或文件对象的指针。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span> *级别*   
可选。 指定要显示在 0 到 7 的详细信息级别越来越多的信息显示为较高的值的小数位数。 若要显示所有可用的详细信息，请提供值为 7。 可以通过发出看到有关级别的详细信息 **！ ks.dump**命令不带任何参数。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
可选。 指定要显示的信息类型。 *标志*可以是以下位的任意组合。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示所有排队的 Irp。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
显示所有挂起的 Irp。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
分析已停止的关系图的怀疑。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>位 3 (0x8)  
显示所有固定状态。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[流式处理的内核调试](kernel-streaming-debugging.md)。

<a name="remarks"></a>备注
-------

**！ Ks.dump**命令识别大多数 AVStream 对象，包括 pin、 筛选器、 工厂、 设备、 管道和流指针。 此命令还可识别某些流类结构，包括流对象、 筛选器实例、 设备扩展和 Srb。

下面是举例 **！ ks.dump**显示筛选器：

```dbgcmd
kd> !dump 829493c4
Filter object 829493c4 [CKsFilter = 82949350]
    Descriptor     f7a233c8:
    Context        829dce28
```

下面是举例 **！ ks.dump**显示 pin:

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

下表中包含此显示一些重要部分。

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
<td align="left"><p>Pin 的状态请求的输入。 如果不同于 ClientState，这是微型驱动程序将转换到下一步的状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ClientState</p></td>
<td align="left"><p>微型驱动程序是中的实际状态。 这反映了管道的状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ResetState</p></td>
<td align="left"><p>指示对象正在进行刷新。</p>
<p>KSRESET_BEGIN 指示刷新。</p>
<p>KSRESET_END 指示没有刷新。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>状态</p></td>
<td align="left"><p>Pin 的传输到非 AVStream 筛选器的内部状态。</p></td>
</tr>
</tbody>
</table>

 

下面是举例 **！ ks.dump**显示的流类驱动程序：

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

请注意，列出大小都用十六进制数字，然后了在本次在十进制等效值。 下表列出了在此显示中的大小缩写词。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>大小</strong></p></td>
<td align="left"><p><strong>说明</strong></p></td>
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
<td align="left"><p>文件</p></td>
<td align="left"><p>“数据流”，</p></td>
</tr>
<tr class="odd">
<td align="left"><p>f</p></td>
<td align="left"><p>筛选器。 如果筛选器大小为 0，筛选器是单一实例。 如果大于 0，它是多实例。</p></td>
</tr>
</tbody>
</table>

 

 

 





