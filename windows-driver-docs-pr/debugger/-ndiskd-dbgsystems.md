---
title: ndiskd.dbgsystems
description: Ndiskd.dbgsystems 扩展显示，并根据需要更改已启用调试跟踪的 NDIS 子系统。  ndiskd.dbgsystems 具有被取代 WPP 和驱动程序验证程序。
ms.assetid: f36a26b6-18a8-4a01-96c7-99826e6b662f
keywords:
- ndiskd.dbgsystems Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.dbgsystems
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 56354f8347201c637191318919efa66508bec642
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336071"
---
# <a name="ndiskddbgsystems"></a>!ndiskd.dbgsystems


**！ Ndiskd.dbgsystems**扩展显示，并根据需要更改已启用调试跟踪的 NDIS 子系统。

**警告**  
 **！ ndiskd.dbgsystems**已 WPP （Windows 软件跟踪预处理器） 和驱动程序验证程序被取代。 ！ ndiskd 将显示以下警告如果您的目标系统不支持 **！ ndiskd.dbgsystems**。

```console
0: kd> !ndiskd.dbgsystems
    This target does not support tracing through !ndiskd.dbglevel or
    !ndiskd.dbgsystems.
    Learn how to collect traces with WPP
```

如果您单击底部的警告，链接 ！ ndiskd 将为你提供详细信息。

```console
0: kd> !ndiskd.help wpptracing
    WPP traces are fast, flexible, and detailed.  Plus, starting with Windows 8
    and Windows Server 2012, you can automatically decode NDIS traces using the
    symbol file.  Just point TraceView (or tracepdb.exe) at NDIS.PDB, and it
    will be able to get all the TMFs it needs to trace NDIS activity.
    
    If you would like traces to be printed in the debugger window, you use the
    !wmitrace extension.  For example, you might enable traces with this:

    !wmitrace.searchpath c:\path\to\TMF\files
    !wmitrace.start ndis -kd
    !wmitrace.enable ndis {DD7A21E6-A651-46D4-B7C2-66543067B869} -level 4 -flag 0x31f3
```

 

有关 WPP 详细信息，请参阅[WPP 软件跟踪](https://msdn.microsoft.com/windows/hardware/drivers/devtest/wpp-software-tracing)。

有关驱动程序验证程序的详细信息，请参阅[Driver Verifier](https://msdn.microsoft.com/windows/hardware/drivers/devtest/driver-verifier)。

有关 WMI 跟踪的详细信息，请参阅[WMI 跟踪扩展 (Wmitrace.dll)](https://msdn.microsoft.com/library/windows/hardware/ff561362)。

```console
!ndiskd.dbgsystems [-subsystem <any>] 
```

## <a name="span-idddkndiskddbgsystemsdbgspanspan-idddkndiskddbgsystemsdbgspanparameters"></a><span id="ddk__ndiskd_dbgsystems_dbg"></span><span id="DDK__NDISKD_DBGSYSTEMS_DBG"></span>参数


<span id="_______-subsystem______"></span><span id="_______-SUBSYSTEM______"></span> *-subsystem*   
要切换的子系统。

如果选择了多个组件，请用空格分隔它们。 如果重复以前选择的组件，则将关闭切换其调试监视。 可能的值如下：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>值</strong></p></td>
<td align="left"><p><strong>含义</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>INIT</p></td>
<td align="left"><p>跟踪适配器初始化。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>配置</p></td>
<td align="left"><p>跟踪适配器配置。</p></td>
</tr>
<tr class="even">
<td align="left"><p>发送</p></td>
<td align="left"><p>通过网络发送数据的跟踪。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RECV</p></td>
<td align="left"><p>从网络接收数据的跟踪。</p></td>
</tr>
<tr class="even">
<td align="left"><p>协议</p></td>
<td align="left"><p>跟踪的协议操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>将绑定</p></td>
<td align="left"><p>绑定操作的跟踪。</p></td>
</tr>
<tr class="even">
<td align="left"><p>BUS_QUERY</p></td>
<td align="left"><p>跟踪 bus 查询。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>注册表</p></td>
<td align="left"><p>跟踪注册表操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>内存</p></td>
<td align="left"><p>跟踪内存管理。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>筛选器</p></td>
<td align="left"><p>跟踪的筛选器操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>请求</p></td>
<td align="left"><p>跟踪请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WORK_ITEM</p></td>
<td align="left"><p>跟踪工作项操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PNP</p></td>
<td align="left"><p>跟踪即插即用和播放操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PM</p></td>
<td align="left"><p>跟踪电源管理操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>打开</p></td>
<td align="left"><p>打开引用对象的跟踪操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>锁</p></td>
<td align="left"><p>锁定操作的跟踪。</p></td>
</tr>
<tr class="even">
<td align="left"><p>重置</p></td>
<td align="left"><p>重置操作的跟踪。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WMI</p></td>
<td align="left"><p>跟踪 Windows Management Instrumentation 操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NDIS_CO</p></td>
<td align="left"><p>跟踪面向连接的 NDIS。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>引用</p></td>
<td align="left"><p>跟踪引用操作。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="remarks"></a>备注
-------

此扩展适用于仅选中 NDIS.sys。 若要检查 NDIS.sys 的生成信息，请运行[ **！ ndiskd.ndis** ](-ndiskd-ndis.md)扩展。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**!ndiskd.ndis**](-ndiskd-ndis.md)

[WPP 软件跟踪](https://msdn.microsoft.com/windows/hardware/drivers/devtest/wpp-software-tracing)

[驱动程序验证程序](https://msdn.microsoft.com/windows/hardware/drivers/devtest/driver-verifier)

[WMI 跟踪扩展 (Wmitrace.dll)](https://msdn.microsoft.com/library/windows/hardware/ff561362)

 

 






