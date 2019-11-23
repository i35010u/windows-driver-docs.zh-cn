---
title: NDIS 扩展 (Ndiskd.dll)
description: NDIS 扩展 (Ndiskd.dll)
ms.assetid: bf4a7cc2-0116-4d6d-8a6f-2e9dc77d3631
keywords:
- NDIS 扩展（ndiskd）
- ndiskd （NDIS 扩展）
- 扩展，NDIS
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44e8d451dbaa0cc6b4d369a80c55febf09209e2a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834296"
---
# <a name="ndis-extensions-ndiskddll"></a>NDIS 扩展 (Ndiskd.dll)


## <span id="ddk_ndis_extensions_ndiskd_dll__dbg"></span><span id="DDK_NDIS_EXTENSIONS_NDISKD_DLL__DBG"></span>


本部分介绍！ ndiskd 中可用的命令，它是一种可用于调试 NDIS （网络设备接口规范）驱动程序的调试器扩展。 网络驱动程序开发人员可以使用这些命令来查看 Windows 网络堆栈的更大的图片以及其驱动程序与之进行交互的方式。 使用！ ndiskd，你可以查看所有网络适配器（[ **！ ndiskd**](-ndiskd-netadapter.md)）的状态、计算机网络堆栈的可视化关系图（[ **！ ndiskd**](-ndiskd-netreport.md)）、网络适配器上的流量日志（[ **！ netreport**](-ndiskd-nbllog.md)）或所有挂起的 OID 请求（[ **！ ndiskd**](-ndiskd-oid.md)）的列表。

可以在 Ndiskd 中找到命令。 若要加载符号，请在调试器命令窗口中输入 **。** 若要确认符号是否已成功加载，请使用[ **！ lmi ndis**](-lmi.md)扩展，并在底部查找 "已成功加载的符号" 字样。 输出应类似于以下示例：

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

## <a name="span-id_ndiskd_hyperlinksspanspan-id_ndiskd_hyperlinksspanspan-id_ndiskd_hyperlinksspanndiskd-hyperlinks"></a><span id="_ndiskd_Hyperlinks"></span><span id="_ndiskd_hyperlinks"></span><span id="_NDISKD_HYPERLINKS"></span>！ ndiskd 超链接


！ Ndiskd 中的许多扩展命令向你显示其在调试器窗口中显示的结果中的超链接。 这些超链接的文本保留在提供的示例中，以说明在调试对象计算机上运行命令时将看到的确切格式。 其中一些示例还显式地引用了这些链接，以便您可以了解典型的使用流，尽管示例还提供了每个命令的备用命令行形式。

## <a name="span-idcommon_parametersspanspan-idcommon_parametersspanspan-idcommon_parametersspancommon-parameters"></a><span id="Common_Parameters"></span><span id="common_parameters"></span><span id="COMMON_PARAMETERS"></span>通用参数


All！ ndiskd 命令支持以下泛型参数。

<span id="_______-verbose______"></span><span id="_______-VERBOSE______"></span> *-详细*   
显示其他详细信息。

<span id="_______-terse______"></span><span id="_______-TERSE______"></span> *-简要*   
禁止显示某些样本输出。

<span id="_______-static______"></span><span id="_______-STATIC______"></span> *-static*   
禁止显示某些交互式输出。

<span id="_______-dml_0_1______"></span><span id="_______-DML_0_1______"></span> *-dml 0 | 1*   
控制是否启用 DML （调试器标记语言）输出。

<span id="_______-unicode_0_1______"></span><span id="_______-UNICODE_0_1______"></span> *-unicode 0 | 1*   
控制是否允许 Unicode 字符输出。

<span id="_______-indent_N______"></span><span id="_______-indent_n______"></span><span id="_______-INDENT_N______"></span> *-缩进 N*   
每个缩进级别使用*N*个空格。

<span id="_______-force______"></span><span id="_______-FORCE______"></span> *-force*   
覆盖对远程数据稳定的某些安全检查。

<span id="_______-tracedata______"></span><span id="_______-TRACEDATA______"></span> *-tracedata*   
显示要调试的详细跟踪消息！ ndiskd 本身。

## <a name="span-idnet_adapter__ndis_driver__and_general_commandsspanspan-idnet_adapter__ndis_driver__and_general_commandsspanspan-idnet_adapter__ndis_driver__and_general_commandsspannet-adapter-ndis-driver-and-general-commands"></a><span id="Net_Adapter__NDIS_Driver__and_General_Commands"></span><span id="net_adapter__ndis_driver__and_general_commands"></span><span id="NET_ADAPTER__NDIS_DRIVER__AND_GENERAL_COMMANDS"></span>Net Adapter、NDIS 驱动程序和常规命令


以下命令显示有关计算机的网络适配器、网络驱动程序和与网络堆栈（如 rcvqueues、打开、筛选器、Oid 和 RW 锁）相关的常规命令的信息。

-   [ **！ ndiskd. get-netadapter**](-ndiskd-netadapter.md)
-   [ **！ ndiskd. 微型驱动程序**](-ndiskd-minidriver.md)
-   [ **!ndiskd.rcvqueue**](-ndiskd-rcvqueue.md)
-   [ **！ ndiskd**](-ndiskd-protocol.md)
-   [ **!ndiskd.mopen**](-ndiskd-mopen.md)
-   [ **！ ndiskd**](-ndiskd-filter.md)
-   [ **!ndiskd.filterdriver**](-ndiskd-filterdriver.md)
-   [ **！ ndiskd**](-ndiskd-oid.md)
-   [ **!ndiskd.ndisrwlock**](-ndiskd-ndisrwlock.md)
-   [ **!ndiskd.netreport**](-ndiskd-netreport.md)

## <a name="span-idnet_buffer_list_and_net_buffer_commandsspanspan-idnet_buffer_list_and_net_buffer_commandsspanspan-idnet_buffer_list_and_net_buffer_commandsspannet_buffer_list-and-net_buffer-commands"></a><span id="NET_BUFFER_LIST_and_NET_BUFFER_Commands"></span><span id="net_buffer_list_and_net_buffer_commands"></span><span id="NET_BUFFER_LIST_AND_NET_BUFFER_COMMANDS"></span>NET\_BUFFER\_LIST 和 NET\_BUFFER 命令


以下命令显示与[**net\_buffer\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)和[**net\_缓冲**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-structure)结构有关的信息。

-   [ **！ ndiskd. nbl**](-ndiskd-nbl.md)
-   [ **！ ndiskd**](-ndiskd-nb.md)
-   [ **!ndiskd.nblpool**](-ndiskd-nblpool.md)
-   [ **!ndiskd.nbpool**](-ndiskd-nbpool.md)
-   [ **!ndiskd.pendingnbls**](-ndiskd-pendingnbls.md)
-   [ **!ndiskd.nbllog**](-ndiskd-nbllog.md)

## <a name="span-idnetadaptercx_commandsspanspan-idnetadaptercx_commandsspanspan-idnetadaptercx_commandsspannetadaptercx-commands"></a><span id="NetAdapterCx_Commands"></span><span id="netadaptercx_commands"></span><span id="NETADAPTERCX_COMMANDS"></span>NetAdapterCx 命令


以下命令显示与网络适配器 WDF 类扩展（NetAdapterCx）相关的信息，\[LINK TBD\] 及其关联结构，NET\_环形\_缓冲区 \[LINK TBD\] 和 NET\_PACKET \[LINK TBD\]。

-   [ **!ndiskd.cxadapter**](-ndiskd-cxadapter.md)
-   [ **!ndiskd.netqueue**](-ndiskd-netqueue.md)
-   [ **!ndiskd.netrb**](-ndiskd-netrb.md)
-   [ **!ndiskd.netpacket**](-ndiskd-netpacket.md)
-   [ **!ndiskd.netpacketfragment**](-ndiskd-netpacketfragment.md)

## <a name="span-idnetwork_interface_commandsspanspan-idnetwork_interface_commandsspanspan-idnetwork_interface_commandsspannetwork-interface-commands"></a><span id="Network_Interface_Commands"></span><span id="network_interface_commands"></span><span id="NETWORK_INTERFACE_COMMANDS"></span>网络接口命令


以下命令显示与网络接口相关的信息。

-   [ **！ ndiskd**](-ndiskd-interfaces.md)
-   [ **!ndiskd.ifprovider**](-ndiskd-ifprovider.md)

## <a name="span-idndis_packet_commandsspanspan-idndis_packet_commandsspanspan-idndis_packet_commandsspanndis_packet-commands"></a><span id="NDIS_PACKET_Commands"></span><span id="ndis_packet_commands"></span><span id="NDIS_PACKET_COMMANDS"></span>NDIS\_数据包命令


以下命令显示有关[NDIS\_数据包](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))结构的信息。 这些扩展适用于旧的 NDIS 1.x 驱动程序。 NDIS\_数据包结构及其关联的体系结构已弃用。

-   [ **！ ndiskd**](-ndiskd-pkt.md)
-   [ **!ndiskd.pktpools**](-ndiskd-pktpools.md)
-   [ **!ndiskd.findpacket**](-ndiskd-findpacket.md)

## <a name="span-idcondis_commandsspanspan-idcondis_commandsspanspan-idcondis_commandsspancondis-commands"></a><span id="CoNDIS_Commands"></span><span id="condis_commands"></span><span id="CONDIS_COMMANDS"></span>CoNDIS 命令


以下命令显示有关[面向连接的 NDIS](https://docs.microsoft.com/windows-hardware/drivers/network/connection-oriented-ndis)连接的信息。

-   [ **！ ndiskd.vc**](-ndiskd-vc.md)
-   [ **！ ndiskd.af**](-ndiskd-af.md)

## <a name="span-idndis_debugging_commandsspanspan-idndis_debugging_commandsspanspan-idndis_debugging_commandsspanndis-debugging-commands"></a><span id="NDIS_Debugging_Commands"></span><span id="ndis_debugging_commands"></span><span id="NDIS_DEBUGGING_COMMANDS"></span>NDIS 调试命令


以下命令显示与 NDIS refcounts、事件日志、堆栈跟踪和调试跟踪相关的信息。

-   [ **!ndiskd.ndisref**](-ndiskd-ndisref.md)
-   [ **!ndiskd.ndisevent**](-ndiskd-ndisevent.md)
-   [ **!ndiskd.ndisstack**](-ndiskd-ndisstack.md)
-   [ **!ndiskd.dbglevel**](-ndiskd-dbglevel.md)
-   [ **!ndiskd.dbgsystems**](-ndiskd-dbgsystems.md)

## <a name="span-idwdi_commandsspanspan-idwdi_commandsspanspan-idwdi_commandsspanwdi-commands"></a><span id="WDI_Commands"></span><span id="wdi_commands"></span><span id="WDI_COMMANDS"></span>WDI 命令


以下命令显示有关[WDI 微型端口驱动程序](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-design-guide)的信息。

-   [ **!ndiskd.wdiadapter**](-ndiskd-wdiadapter.md)
-   [ **!ndiskd.wdiminidriver**](-ndiskd-wdiminidriver.md)
-   [ **!ndiskd.nwadapter**](-ndiskd-nwadapter.md)

## <a name="span-idndis_and__ndiskd_information_commandsspanspan-idndis_and__ndiskd_information_commandsspanspan-idndis_and__ndiskd_information_commandsspanndis-and-ndiskd-information-commands"></a><span id="NDIS_and__ndiskd_Information_Commands"></span><span id="ndis_and__ndiskd_information_commands"></span><span id="NDIS_AND__NDISKD_INFORMATION_COMMANDS"></span>NDIS 和！ ndiskd 信息命令


以下命令显示有关 ndiskd 和的信息。

-   [ **！ ndiskd**](-ndiskd-ndis.md)
-   [ **!ndiskd.ndiskdversion**](-ndiskd-ndiskdversion.md)

## <a name="span-idmiscellaneous_commandsspanspan-idmiscellaneous_commandsspanspan-idmiscellaneous_commandsspanmiscellaneous-commands"></a><span id="Miscellaneous_Commands"></span><span id="miscellaneous_commands"></span><span id="MISCELLANEOUS_COMMANDS"></span>其他命令


-   [ **!ndiskd.ifstacktable**](-ndiskd-ifstacktable.md)
-   [ **！ ndiskd**](-ndiskd-compartments.md)
-   [ **!ndiskd.ndisslot**](-ndiskd-ndisslot.md)

## <a name="span-idrelated_topicsspanspan-idrelated_topicsspanspan-idrelated_topicsspanrelated-topics"></a><span id="Related_Topics"></span><span id="related_topics"></span><span id="RELATED_TOPICS"></span>相关主题


有关设计适用于 Windows Vista 和更高版本的 NDIS 驱动程序的详细信息，请参阅[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)。

有关适用于 Windows Vista 和更高版本的 NDIS 驱动程序参考的详细信息，请参阅[Windows vista 和更高版本的网络参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。

有关使用！ ndiskd 调试器命令调试网络堆栈的演示，请参阅[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)。

 

 






