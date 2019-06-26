---
title: NDIS 扩展 (Ndiskd.dll)
description: NDIS 扩展 (Ndiskd.dll)
ms.assetid: bf4a7cc2-0116-4d6d-8a6f-2e9dc77d3631
keywords:
- NDIS 扩展 (ndiskd.dll)
- ndiskd.dll （NDIS 扩展）
- 扩展 NDIS
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70b8ff4added860de71ced21c2e63ec9de2fcb77
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366463"
---
# <a name="ndis-extensions-ndiskddll"></a>NDIS 扩展 (Ndiskd.dll)


## <span id="ddk_ndis_extensions_ndiskd_dll__dbg"></span><span id="DDK_NDIS_EXTENSIONS_NDISKD_DLL__DBG"></span>


本部分介绍了中的可用命令 ！ ndiskd，调试器扩展，可用于调试的 NDIS （网络设备接口规范） 驱动程序。 这些命令启用网络驱动程序开发人员若要查看更大的图片的 Windows 网络堆栈和其驱动程序如何与之进行交互。 使用 ！ ndiskd，可以看到所有网络适配器的状态 ([ **！ ndiskd.netadapter**](-ndiskd-netadapter.md))，计算机的网络堆栈的可视化关系图 ([ **！ ndiskd.netreport**](-ndiskd-netreport.md))，流量的网络适配器上的日志 ([ **！ ndiskd.nbllog**](-ndiskd-nbllog.md))，或所有挂起的 OID 请求的列表 ([ **！ ndiskd.oid**](-ndiskd-oid.md)).

可以在 Ndiskd.dll 中找到命令。 若要加载的符号，请输入 **.reload /f ndis.sys**调试器命令窗口中。 若要确认已成功加载符号，请使用[ **！ lmi ndis** ](-lmi.md)扩展并查找短语"符号加载已成功"到底部。 输出应类似于下面的示例：

```dbgcmd
3: kd> !lmi ndis
Loaded Module Info: [ndis] 
         Module: ndis
   Base Address: fffff80e2e150000
     Image Name: ndis.sys
   Machine Type: 34404 (X64)
     Time Stamp: 57f4c58d Wed Oct  5 02:19:09 2016
           Size: 128000
       CheckSum: 1213f7
Characteristics: 22  
Debug Data Dirs: Type  Size     VA  Pointer
             CODEVIEW    21, 7b1b8,   79fb8 RSDS - GUID: {06A2E58C-996D-4419-81A0-BB293BD63BCA}
               Age: 1, Pdb: ndis.pdb
                   ??   880, 7b1dc,   79fdc [Data not mapped]
     Image Type: MEMORY   - Image read successfully from loaded memory.
    Symbol Type: PDB      - Symbols loaded successfully from image header.
                 c:\Debuggers\sym\ndis.pdb\06A2E58C996D441981A0BB293BD63BCA1\ndis.pdb
       Compiler: Linker - front end [0.0 bld 0] - back end [14.0 bld 23917]
    Load Report: private symbols & lines, source indexed 
                 c:\Debuggers\sym\ndis.pdb\06A2E58C996D441981A0BB293BD63BCA1\ndis.pdb
```

## <a name="span-idndiskdhyperlinksspanspan-idndiskdhyperlinksspanspan-idndiskdhyperlinksspanndiskd-hyperlinks"></a><span id="_ndiskd_Hyperlinks"></span><span id="_ndiskd_hyperlinks"></span><span id="_NDISKD_HYPERLINKS"></span>！ ndiskd 超链接


中的扩展命令的许多 ！ ndiskd 为你提供它们在调试器窗口中显示的结果中的超链接。 这些超链接的文本已保留在提供用于说明在调试对象上运行命令时将看到的确切格式的示例。 一些示例还指显式单击这些链接以便您可以了解典型用法流，尽管这些示例还提供备用的命令行形式的每个命令。

## <a name="span-idcommonparametersspanspan-idcommonparametersspanspan-idcommonparametersspancommon-parameters"></a><span id="Common_Parameters"></span><span id="common_parameters"></span><span id="COMMON_PARAMETERS"></span>通用参数


所有 ！ ndiskd 命令支持以下泛型参数。

<span id="_______-verbose______"></span><span id="_______-VERBOSE______"></span> *-verbose*   
显示更多详细信息。

<span id="_______-terse______"></span><span id="_______-TERSE______"></span> *-terse*   
禁止显示某些样本输出。

<span id="_______-static______"></span><span id="_______-STATIC______"></span> *-static*   
禁止显示某些交互式输出。

<span id="_______-dml_0_1______"></span><span id="_______-DML_0_1______"></span> *-dml 0|1*   
控制是否启用 DML （调试器标记语言） 输出。

<span id="_______-unicode_0_1______"></span><span id="_______-UNICODE_0_1______"></span> *-unicode 0|1*   
控制是否允许 Unicode 字符输出。

<span id="_______-indent_N______"></span><span id="_______-indent_n______"></span><span id="_______-INDENT_N______"></span> *-indent N*   
使用*N*每个级别的缩进的空格。

<span id="_______-force______"></span><span id="_______-FORCE______"></span> *-force*   
重写某些安全检查在远程数据的完整性。

<span id="_______-tracedata______"></span><span id="_______-TRACEDATA______"></span> *-tracedata*   
显示要调试的详细跟踪消息 ！ ndiskd 本身。

## <a name="span-idnetadapterndisdriverandgeneralcommandsspanspan-idnetadapterndisdriverandgeneralcommandsspanspan-idnetadapterndisdriverandgeneralcommandsspannet-adapter-ndis-driver-and-general-commands"></a><span id="Net_Adapter__NDIS_Driver__and_General_Commands"></span><span id="net_adapter__ndis_driver__and_general_commands"></span><span id="NET_ADAPTER__NDIS_DRIVER__AND_GENERAL_COMMANDS"></span>网络适配器、 NDIS 驱动程序和常规命令


下面的命令显示有关计算机的网络适配器、 网络驱动程序和常规命令 （如 rcvqueues、 打开、 筛选器、 Oid，和 RW 锁定） 的网络堆栈与相关联的信息。

-   [ **!ndiskd.netadapter**](-ndiskd-netadapter.md)
-   [ **!ndiskd.minidriver**](-ndiskd-minidriver.md)
-   [ **!ndiskd.rcvqueue**](-ndiskd-rcvqueue.md)
-   [ **!ndiskd.protocol**](-ndiskd-protocol.md)
-   [ **!ndiskd.mopen**](-ndiskd-mopen.md)
-   [ **!ndiskd.filter**](-ndiskd-filter.md)
-   [ **!ndiskd.filterdriver**](-ndiskd-filterdriver.md)
-   [ **!ndiskd.oid**](-ndiskd-oid.md)
-   [ **!ndiskd.ndisrwlock**](-ndiskd-ndisrwlock.md)
-   [ **!ndiskd.netreport**](-ndiskd-netreport.md)

## <a name="span-idnetbufferlistandnetbuffercommandsspanspan-idnetbufferlistandnetbuffercommandsspanspan-idnetbufferlistandnetbuffercommandsspannetbufferlist-and-netbuffer-commands"></a><span id="NET_BUFFER_LIST_and_NET_BUFFER_Commands"></span><span id="net_buffer_list_and_net_buffer_commands"></span><span id="NET_BUFFER_LIST_AND_NET_BUFFER_COMMANDS"></span>NET\_缓冲区\_列表和 NET\_缓冲区命令


以下命令将显示与相关的信息[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)并[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-structure)结构。

-   [ **!ndiskd.nbl**](-ndiskd-nbl.md)
-   [ **!ndiskd.nb**](-ndiskd-nb.md)
-   [ **!ndiskd.nblpool**](-ndiskd-nblpool.md)
-   [ **!ndiskd.nbpool**](-ndiskd-nbpool.md)
-   [ **!ndiskd.pendingnbls**](-ndiskd-pendingnbls.md)
-   [ **!ndiskd.nbllog**](-ndiskd-nbllog.md)

## <a name="span-idnetadaptercxcommandsspanspan-idnetadaptercxcommandsspanspan-idnetadaptercxcommandsspannetadaptercx-commands"></a><span id="NetAdapterCx_Commands"></span><span id="netadaptercx_commands"></span><span id="NETADAPTERCX_COMMANDS"></span>NetAdapterCx 命令


以下命令将显示与网络适配器 WDF 类扩展 (NetAdapterCx) 相关的信息\[LINK TBD\]及其关联的结构，NET\_环\_缓冲区\[LINK TBD\]和 NET\_数据包\[链接 TBD\]。

-   [ **!ndiskd.cxadapter**](-ndiskd-cxadapter.md)
-   [ **!ndiskd.netqueue**](-ndiskd-netqueue.md)
-   [ **!ndiskd.netrb**](-ndiskd-netrb.md)
-   [ **!ndiskd.netpacket**](-ndiskd-netpacket.md)
-   [ **!ndiskd.netpacketfragment**](-ndiskd-netpacketfragment.md)

## <a name="span-idnetworkinterfacecommandsspanspan-idnetworkinterfacecommandsspanspan-idnetworkinterfacecommandsspannetwork-interface-commands"></a><span id="Network_Interface_Commands"></span><span id="network_interface_commands"></span><span id="NETWORK_INTERFACE_COMMANDS"></span>网络接口命令


以下命令将显示网络接口相关的信息。

-   [ **!ndiskd.interfaces**](-ndiskd-interfaces.md)
-   [ **!ndiskd.ifprovider**](-ndiskd-ifprovider.md)

## <a name="span-idndispacketcommandsspanspan-idndispacketcommandsspanspan-idndispacketcommandsspanndispacket-commands"></a><span id="NDIS_PACKET_Commands"></span><span id="ndis_packet_commands"></span><span id="NDIS_PACKET_COMMANDS"></span>NDIS\_数据包命令


以下命令显示有关的信息[NDIS\_数据包](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))结构。 这些扩展是旧的 NDIS 5.x 驱动程序。 NDIS\_数据包结构和其关联的体系结构已被弃用。

-   [ **!ndiskd.pkt**](-ndiskd-pkt.md)
-   [ **!ndiskd.pktpools**](-ndiskd-pktpools.md)
-   [ **!ndiskd.findpacket**](-ndiskd-findpacket.md)

## <a name="span-idcondiscommandsspanspan-idcondiscommandsspanspan-idcondiscommandsspancondis-commands"></a><span id="CoNDIS_Commands"></span><span id="condis_commands"></span><span id="CONDIS_COMMANDS"></span>CoNDIS 命令


以下命令显示有关的信息[Connection-Oriented NDIS](https://docs.microsoft.com/windows-hardware/drivers/network/connection-oriented-ndis)连接。

-   [ **!ndiskd.vc**](-ndiskd-vc.md)
-   [ **!ndiskd.af**](-ndiskd-af.md)

## <a name="span-idndisdebuggingcommandsspanspan-idndisdebuggingcommandsspanspan-idndisdebuggingcommandsspanndis-debugging-commands"></a><span id="NDIS_Debugging_Commands"></span><span id="ndis_debugging_commands"></span><span id="NDIS_DEBUGGING_COMMANDS"></span>NDIS 调试命令


以下命令将显示与 NDIS refcounts、 事件日志、 堆栈跟踪和调试跟踪相关的信息。

-   [ **!ndiskd.ndisref**](-ndiskd-ndisref.md)
-   [ **!ndiskd.ndisevent**](-ndiskd-ndisevent.md)
-   [ **!ndiskd.ndisstack**](-ndiskd-ndisstack.md)
-   [ **!ndiskd.dbglevel**](-ndiskd-dbglevel.md)
-   [ **!ndiskd.dbgsystems**](-ndiskd-dbgsystems.md)

## <a name="span-idwdicommandsspanspan-idwdicommandsspanspan-idwdicommandsspanwdi-commands"></a><span id="WDI_Commands"></span><span id="wdi_commands"></span><span id="WDI_COMMANDS"></span>WDI 命令


以下命令显示有关的信息[WDI 微型端口驱动程序](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-design-guide)。

-   [ **!ndiskd.wdiadapter**](-ndiskd-wdiadapter.md)
-   [ **!ndiskd.wdiminidriver**](-ndiskd-wdiminidriver.md)
-   [ **!ndiskd.nwadapter**](-ndiskd-nwadapter.md)

## <a name="span-idndisandndiskdinformationcommandsspanspan-idndisandndiskdinformationcommandsspanspan-idndisandndiskdinformationcommandsspanndis-and-ndiskd-information-commands"></a><span id="NDIS_and__ndiskd_Information_Commands"></span><span id="ndis_and__ndiskd_information_commands"></span><span id="NDIS_AND__NDISKD_INFORMATION_COMMANDS"></span>NDIS 和 ！ ndiskd 信息命令


下面的命令显示有关 NDIS.sys 和 ndiskd.dll 的信息。

-   [ **!ndiskd.ndis**](-ndiskd-ndis.md)
-   [ **!ndiskd.ndiskdversion**](-ndiskd-ndiskdversion.md)

## <a name="span-idmiscellaneouscommandsspanspan-idmiscellaneouscommandsspanspan-idmiscellaneouscommandsspanmiscellaneous-commands"></a><span id="Miscellaneous_Commands"></span><span id="miscellaneous_commands"></span><span id="MISCELLANEOUS_COMMANDS"></span>杂项命令


-   [ **!ndiskd.ifstacktable**](-ndiskd-ifstacktable.md)
-   [ **!ndiskd.compartments**](-ndiskd-compartments.md)
-   [ **!ndiskd.ndisslot**](-ndiskd-ndisslot.md)

## <a name="span-idrelatedtopicsspanspan-idrelatedtopicsspanspan-idrelatedtopicsspanrelated-topics"></a><span id="Related_Topics"></span><span id="related_topics"></span><span id="RELATED_TOPICS"></span>相关的主题


详细了解设计 NDIS 驱动程序适用于 Windows Vista 及更高版本，请参阅[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)。

有关适用于 Windows Vista 及更高版本的 NDIS 驱动程序的引用的详细信息，请参阅[Windows Vista 和更高版本的网络参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)。

有关使用的演示 ！ ndiskd 调试器命令调试网络堆栈，请参阅[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)。

 

 






