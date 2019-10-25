---
title: ndiskd.dbgsystems
description: Ndiskd. dbgsystems 扩展显示，并选择性地更改启用了调试跟踪的 NDIS 子系统。  ndiskd 已被 WPP 和驱动程序验证程序取代。
ms.assetid: f36a26b6-18a8-4a01-96c7-99826e6b662f
keywords:
- ndiskd dbgsystems Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.dbgsystems
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b47b5cf4b4296706d90c6f8ca5b3f291f2cc59ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826672"
---
# <a name="ndiskddbgsystems"></a>!ndiskd.dbgsystems


**！ Ndiskd dbgsystems**扩展显示，并选择性地更改启用了调试跟踪的 NDIS 子系统。

**警告**  
 **！ NDISKD**已被 WPP （Windows 软件跟踪预处理器）和驱动程序验证程序取代。 ！如果目标系统不支持 **！ ndiskd dbgsystems**，ndiskd 将为你提供以下警告。

```console
0: kd> !ndiskd.dbgsystems
    This target does not support tracing through !ndiskd.dbglevel or
    !ndiskd.dbgsystems.
    Learn how to collect traces with WPP
```

如果单击警告底部的链接，！ ndiskd 将会获得详细信息。

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

 

有关 WPP 的详细信息，请参阅[Wpp 软件跟踪](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)。

有关驱动程序验证程序的详细信息，请参阅[驱动程序验证](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)器。

有关 WMI 跟踪的详细信息，请参阅[Wmi 跟踪扩展（Wmitrace）](https://docs.microsoft.com/windows-hardware/drivers/debugger/wmi-tracing-extensions--wmitrace-dll-)。

```console
!ndiskd.dbgsystems [-subsystem <any>] 
```

## <a name="span-idddk__ndiskd_dbgsystems_dbgspanspan-idddk__ndiskd_dbgsystems_dbgspanparameters"></a><span id="ddk__ndiskd_dbgsystems_dbg"></span><span id="DDK__NDISKD_DBGSYSTEMS_DBG"></span>Parameters


<span id="_______-subsystem______"></span><span id="_______-SUBSYSTEM______"></span> *-子系统*   
要切换的子系统。

如果选择了多个组件，请用空格分隔它们。 如果重复以前选择的组件，则将关闭其调试监视。 可能的值如下：

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
<td align="left"><p>CONFIG.XML</p></td>
<td align="left"><p>跟踪适配器配置。</p></td>
</tr>
<tr class="even">
<td align="left"><p>发送</p></td>
<td align="left"><p>跟踪通过网络发送数据。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RECV</p></td>
<td align="left"><p>跟踪从网络接收数据。</p></td>
</tr>
<tr class="even">
<td align="left"><p>协议</p></td>
<td align="left"><p>跟踪协议操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>绑定</p></td>
<td align="left"><p>跟踪绑定操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>BUS_QUERY</p></td>
<td align="left"><p>跟踪总线查询。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>REGISTRY</p></td>
<td align="left"><p>跟踪注册表操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>记忆</p></td>
<td align="left"><p>跟踪内存管理。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>筛选器</p></td>
<td align="left"><p>跟踪筛选器操作。</p></td>
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
<td align="left"><p>跟踪即插即用操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>下午</p></td>
<td align="left"><p>跟踪电源管理操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>未</p></td>
<td align="left"><p>跟踪打开引用对象的操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>住</p></td>
<td align="left"><p>跟踪锁定操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>&</p></td>
<td align="left"><p>跟踪重置操作。</p></td>
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
<td align="left"><p>对</p></td>
<td align="left"><p>跟踪引用操作。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Ndiskd

<a name="remarks"></a>备注
-------

此扩展仅适用于已检查的 sys.databases。 若要查看 ndiskd 的生成信息，请运行[ **！** ](-ndiskd-ndis.md)

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展（Ndiskd）** ](ndis-extensions--ndiskd-dll-.md)

[ **！ ndiskd。帮助**](-ndiskd-help.md)

[ **！ ndiskd**](-ndiskd-ndis.md)

[WPP 软件跟踪](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)

[驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)

[WMI 跟踪扩展（Wmitrace）](https://docs.microsoft.com/windows-hardware/drivers/debugger/wmi-tracing-extensions--wmitrace-dll-)

 

 






