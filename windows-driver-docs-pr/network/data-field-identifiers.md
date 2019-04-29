---
title: 数据字段标识符
description: 本部分介绍 Windows 筛选平台标注驱动程序的数据字段标识符。
ms.assetid: 6e617ef4-807b-4564-8b95-b289edfee8d2
keywords:
- 数据字段标识符网络驱动程序
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 197da2051e3dac8a84863ff617b4782f72857891
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372697"
---
# <a name="data-field-identifiers"></a>数据字段标识符

运行时筛选层是与数据字段的标识符相关联。 这些标识符表示一的组声明为中 Fwpsk.h FWPS_FIELDS_XXX 枚举的常量值。

下表列出了运行时筛选层和关联的数据字段枚举。

<table>
<tr>
<th>
运行时筛选层 </th>
<th>
数据字段枚举 </th>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_INBOUND_IPPACKET_V4 FWPS_LAYER_INBOUND_IPPACKET_V4_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551287(v=vs.85).aspx"><b> FWPS_FIELDS_INBOUND_IPPACKET_V4</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_INBOUND_IPPACKET_V6 FWPS_LAYER_INBOUND_IPPACKET_V6_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551289(v=vs.85).aspx"><b> FWPS_FIELDS_INBOUND_IPPACKET_V6</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_OUTBOUND_IPPACKET_V4 FWPS_LAYER_OUTBOUND_IPPACKET_V4_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551329(v=vs.85).aspx"><b> FWPS_FIELDS_OUTBOUND_IPPACKET_V4</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_OUTBOUND_IPPACKET_V6 FWPS_LAYER_OUTBOUND_IPPACKET_V6_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551331(v=vs.85).aspx"><b> FWPS_FIELDS_OUTBOUND_IPPACKET_V6</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_IPFORWARD_V4 FWPS_LAYER_IPFORWARD_V4_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551297(v=vs.85).aspx"><b>FWPS_FIELDS_IPFORWARD_V4</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_IPFORWARD_V6 FWPS_LAYER_IPFORWARD_V6_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551299(v=vs.85).aspx"><b>FWPS_FIELDS_IPFORWARD_V6</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_INBOUND_TRANSPORT_V4 FWPS_LAYER_INBOUND_TRANSPORT_V4_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551293(v=vs.85).aspx"><b> FWPS_FIELDS_INBOUND_TRANSPORT_V4</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_INBOUND_TRANSPORT_V6 FWPS_LAYER_INBOUND_TRANSPORT_V6_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551294(v=vs.85).aspx"><b> FWPS_FIELDS_INBOUND_TRANSPORT_V6</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_OUTBOUND_TRANSPORT_V4 FWPS_LAYER_OUTBOUND_TRANSPORT_V4_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551335(v=vs.85).aspx"><b> FWPS_FIELDS_OUTBOUND_TRANSPORT_V4</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_OUTBOUND_TRANSPORT_V6 FWPS_LAYER_OUTBOUND_TRANSPORT_V6_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551338(v=vs.85).aspx"><b> FWPS_FIELDS_OUTBOUND_TRANSPORT_V6</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_STREAM_V4 FWPS_LAYER_STREAM_V4_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552384(v=vs.85).aspx"><b>FWPS_FIELDS_STREAM_V4</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_STREAM_V6 FWPS_LAYER_STREAM_V6_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552385(v=vs.85).aspx"><b>FWPS_FIELDS_STREAM_V6</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_DATAGRAM_DATA_V4 FWPS_LAYER_DATAGRAM_DATA_V4_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551274(v=vs.85).aspx"><b>FWPS_FIELDS_DATAGRAM_DATA_V4</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_DATAGRAM_DATA_V6 FWPS_LAYER_DATAGRAM_DATA_V6_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551276(v=vs.85).aspx"><b>FWPS_FIELDS_DATAGRAM_DATA_V6</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_STREAM_PACKET_V4</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552379(v=vs.85).aspx"><b>FWPS_FIELDS_STREAM_PACKET_V4</b></a></p>
<div class="alert"><b>请注意</b>  Windows 7 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_STREAM_PACKET_V6</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552383(v=vs.85).aspx"><b>FWPS_FIELDS_STREAM_PACKET_V6</b></a></p>
<div class="alert"><b>请注意</b>  Windows 7 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_INBOUND_ICMP_ERROR_V4 FWPS_LAYER_INBOUND_ICMP_ERROR_V4_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551283(v=vs.85).aspx"><b> FWPS_FIELDS_INBOUND_ICMP_ERROR_V4</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_INBOUND_ICMP_ERROR_V6 FWPS_LAYER_INBOUND_ICMP_ERROR_V6_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551285(v=vs.85).aspx"><b> FWPS_FIELDS_INBOUND_ICMP_ERROR_V6</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_OUTBOUND_ICMP_ERROR_V4 FWPS_LAYER_OUTBOUND_ICMP_ERROR_V4_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551324(v=vs.85).aspx"><b> FWPS_FIELDS_OUTBOUND_ICMP_ERROR_V4</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_OUTBOUND_ICMP_ERROR_V6 FWPS_LAYER_OUTBOUND_ICMP_ERROR_V6_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551327(v=vs.85).aspx"><b> FWPS_FIELDS_OUTBOUND_ICMP_ERROR_V6</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_ALE_RESOURCE_ASSIGNMENT_V4 FWPS_LAYER_ALE_RESOURCE_ASSIGNMENT_V4_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551266(v=vs.85).aspx"><b> FWPS_FIELDS_ALE_RESOURCE_ASSIGNMENT_V4</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_ALE_RESOURCE_ASSIGNMENT_V6 FWPS_LAYER_ALE_RESOURCE_ASSIGNMENT_V6_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551267(v=vs.85).aspx"><b> FWPS_FIELDS_ALE_RESOURCE_ASSIGNMENT_V6</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_ALE_RESOURCE_RELEASE_V4</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551269(v=vs.85).aspx"><b> FWPS_FIELDS_ALE_RESOURCE_RELEASE_V4</b></a></p>
<div class="alert"><b>请注意</b>  Windows 7 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_ALE_RESOURCE_RELEASE_V6</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551272(v=vs.85).aspx"><b> FWPS_FIELDS_ALE_RESOURCE_RELEASE_V6</b></a></p>
<div class="alert"><b>请注意</b>  Windows 7 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_ALE_ENDPOINT_CLOSURE_V4</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551256(v=vs.85).aspx"><b> FWPS_FIELDS_ALE_ENDPOINT_CLOSURE_V4</b></a></p>
<div class="alert"><b>请注意</b>  Windows 7 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_ALE_ENDPOINT_CLOSURE_V6</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551258(v=vs.85).aspx"><b> FWPS_FIELDS_ALE_ENDPOINT_CLOSURE_V6</b></a></p>
<div class="alert"><b>请注意</b>  Windows 7 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_ALE_AUTH_LISTEN_V4 FWPS_LAYER_ALE_AUTH_LISTEN_V4_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551240(v=vs.85).aspx"><b> FWPS_FIELDS_ALE_AUTH_LISTEN_V4</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_ALE_AUTH_LISTEN_V6 FWPS_LAYER_ALE_AUTH_LISTEN_V6_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551242(v=vs.85).aspx"><b> FWPS_FIELDS_ALE_AUTH_LISTEN_V6</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V4 FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V4_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551245(v=vs.85).aspx"><b> FWPS_FIELDS_ALE_AUTH_RECV_ACCEPT_V4</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V6 FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V6_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551246(v=vs.85).aspx"><b> FWPS_FIELDS_ALE_AUTH_RECV_ACCEPT_V6</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_ALE_BIND_REDIRECT_V4</p>
</td>
<td>
<p>
<dl>
<dt><a href="https://msdn.microsoft.com/library/windows/hardware/ff551247(v=vs.85).aspx"><b> FWPS_FIELDS_ALE_BIND_REDIRECT_V4</b></a></dt>
<dt>
<div class="alert"><b>请注意</b>  Windows 7 和更高版本的 Windows 中受支持。</div>
<div> </div>
</dt>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_ALE_BIND_REDIRECT_V6</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551249(v=vs.85).aspx"><b> FWPS_FIELDS_ALE_BIND_REDIRECT_V6</b></a></p>
<div class="alert"><b>请注意</b>  Windows 7 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_ALE_CONNECT_REDIRECT_V4</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551251(v=vs.85).aspx"><b> FWPS_FIELDS_ALE_CONNECT_REDIRECT_V4</b></a></p>
<div class="alert"><b>请注意</b>  Windows 7 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_ALE_CONNECT_REDIRECT_V6</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551254(v=vs.85).aspx"><b> FWPS_FIELDS_ALE_CONNECT_REDIRECT_V6</b></a></p>
<div class="alert"><b>请注意</b>  Windows 7 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_ALE_AUTH_CONNECT_V4 FWPS_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551238(v=vs.85).aspx"><b> FWPS_FIELDS_ALE_AUTH_CONNECT_V4</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_ALE_AUTH_CONNECT_V6 FWPS_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551239(v=vs.85).aspx"><b> FWPS_FIELDS_ALE_AUTH_CONNECT_V6</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_ALE_FLOW_ESTABLISHED_V4 FWPS_LAYER_ALE_FLOW_ESTABLISHED_V4_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551261(v=vs.85).aspx"><b> FWPS_FIELDS_ALE_FLOW_ESTABLISHED_V4</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_ALE_FLOW_ESTABLISHED_V6 FWPS_LAYER_ALE_FLOW_ESTABLISHED_V6_DISCARD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551263(v=vs.85).aspx"><b> FWPS_FIELDS_ALE_FLOW_ESTABLISHED_V6</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_NAME_RESOLUTION_CACHE_V4</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551316(v=vs.85).aspx"><b> FWPS_FIELDS_NAME_RESOLUTION_CACHE_V4</b></a></p>
<div class="alert"><b>请注意</b>  Windows 7 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_NAME_RESOLUTION_CACHE_V6</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551320(v=vs.85).aspx"><b> FWPS_FIELDS_NAME_RESOLUTION_CACHE_V6</b></a></p>
<div class="alert"><b>请注意</b>  Windows 7 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_INBOUND_MAC_FRAME_ETHERNET</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551291(v=vs.85).aspx"><b> FWPS_FIELDS_INBOUND_MAC_FRAME_ETHERNET</b></a></p>
<div class="alert"><b>请注意</b>  支持<i>Windows 8</i>和更高版本的 Windows。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_OUTBOUND_MAC_FRAME_ETHERNET</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551334(v=vs.85).aspx"><b> FWPS_FIELDS_OUTBOUND_MAC_FRAME_ETHERNET</b></a></p>
<div class="alert"><b>请注意</b>  支持<i>Windows 8</i>和更高版本的 Windows。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>
FWPM_LAYER_INBOUND_MAC_FRAME_NATIVE </p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439728(v=vs.85).aspx"><b>FWPS_FIELDS_INBOUND_MAC_FRAME_NATIVE</b></a></p>
<div class="alert"><b>请注意</b>  支持<i>Windows 8</i>和更高版本的 Windows。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_OUTBOUND_MAC_FRAME_NATIVE</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439757(v=vs.85).aspx"><b>FWPS_FIELDS_OUTBOUND_MAC_FRAME_NATIVE</b></a></p>
<div class="alert"><b>请注意</b>  支持<i>Windows 8</i>和更高版本的 Windows。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_IPSEC_KM_DEMUX_V4</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551301(v=vs.85).aspx"><b> FWPS_FIELDS_IPSEC_KM_DEMUX_V4</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_IPSEC_KM_DEMUX_V6</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551304(v=vs.85).aspx"><b> FWPS_FIELDS_IPSEC_KM_DEMUX_V6</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_IPSEC_V4</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551305(v=vs.85).aspx"><b>FWPS_FIELDS_IPSEC_V4</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_IPSEC_V6</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551307(v=vs.85).aspx"><b>FWPS_FIELDS_IPSEC_V6</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_IKEEXT_V4</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551278(v=vs.85).aspx"><b>FWPS_FIELDS_IKEEXT_V4</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_IKEEXT_V6</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551281(v=vs.85).aspx"><b>FWPS_FIELDS_IKEEXT_V6</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_RPC_UM</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552376(v=vs.85).aspx"><b>FWPS_FIELDS_RPC_UM</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_RPC_EPMAP</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551339(v=vs.85).aspx"><b>FWPS_FIELDS_RPC_EPMAP</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_RPC_EP_ADD</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552370(v=vs.85).aspx"><b>FWPS_FIELDS_RPC_EP_ADD</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_RPC_PROXY_CONN</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552372(v=vs.85).aspx"><b>FWPS_FIELDS_RPC_PROXY_CONN</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_RPC_PROXY_IF</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552374(v=vs.85).aspx"><b>FWPS_FIELDS_RPC_PROXY_IF_IF</b></a></p>
</td>
</tr>
<tr>
<td>
<p>
FWPS_LAYER_KM_AUTHORIZATION</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551312(v=vs.85).aspx"><b>FWPS_FIELDS_KM_AUTHORIZATION</b></a></p>
<div class="alert"><b>请注意</b>  Windows 7 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INGRESS_VSWITCH_ETHERNET</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439733(v=vs.85).aspx"><b>FWPS_FIELDS_INGRESS_VSWITCH_ETHERNET </b></a></p>
<div class="alert"><b>请注意</b>  支持<i>Windows 8</i>和更高版本的 Windows。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_EGRESS_VSWITCH_ETHERNET</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439709(v=vs.85).aspx"><b>FWPS_FIELDS_EGRESS_VSWITCH_ETHERNET </b></a></p>
<div class="alert"><b>请注意</b>  支持<i>Windows 8</i>和更高版本的 Windows。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INGRESS_VSWITCH_TRANSPORT_V4</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439738(v=vs.85).aspx"><b>FWPS_FIELDS_INGRESS_VSWITCH_TRANSPORT_V4 </b></a></p>
<div class="alert"><b>请注意</b>  支持<i>Windows 8</i>和更高版本的 Windows。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>WPS_LAYER_INGRESS_VSWITCH_TRANSPORT_V6</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439745(v=vs.85).aspx"><b>FWPS_FIELDS_INGRESS_VSWITCH_TRANSPORT_V6 </b></a></p>
<div class="alert"><b>请注意</b>  支持<i>Windows 8</i>和更高版本的 Windows。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_EGRESS_VSWITCH_TRANSPORT_V4</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439715(v=vs.85).aspx"><b>FWPS_FIELDS_EGRESS_VSWITCH_TRANSPORT_V4 </b></a></p>
<div class="alert"><b>请注意</b>  支持<i>Windows 8</i>和更高版本的 Windows。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_EGRESS_VSWITCH_TRANSPORT_V6</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439721(v=vs.85).aspx"><b>FWPS_FIELDS_EGRESS_VSWITCH_TRANSPORT_V6 </b></a></p>
<div class="alert"><b>请注意</b>  支持<i>Windows 8</i>和更高版本的 Windows。</div>
<div> </div>
</td>
</tr>
</table>

