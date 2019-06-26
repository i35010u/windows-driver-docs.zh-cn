---
title: 将 SDP 记录转换为树状结构
description: 将 SDP 记录转换为树状结构
ms.assetid: 762cf68b-0082-4b9e-8f24-ff19ecf6f8bd
keywords:
- 蓝牙 WDK，SDP 服务器通信
- SDP WDK 蓝牙
- 服务发现协议 WDK 蓝牙
- 浏览服务 WDK 蓝牙
- 搜索服务 WDK 蓝牙
- 浏览 WDK 蓝牙的服务
- 转换 SDP 记录
- 从 SDP 记录 WDK 蓝牙的树结构
- SdpConvertStreamToTree
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f0d7e6ffd12a1b3fdfdd5ab07c295d384e77f65
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354018"
---
# <a name="converting-sdp-records-to-a-tree-structure"></a>将 SDP 记录转换为树状结构


服务发现协议 (SDP) 记录以复杂的二进制流进行编码。 若要启用配置文件驱动程序来分析 SDP 记录更多轻松，蓝牙驱动程序堆栈提供多个配置文件驱动程序可以使用 SDP 记录流转换为分层树形结构并切换回的函数。

客户端配置文件驱动程序可以使用[ **SdpConvertStreamToTree** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthsdpddi/nc-bthsdpddi-pconvertstreamtotree)函数将 SDP 记录转换为树状结构。 调用结果的 SDP 记录的树表示形式**SdpConvertStreamToTree**函数包含一个包含与 SDP 记录关联的所有信息的根节点定义的[ **SDP\_树\_根\_节点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdpnode/ns-sdpnode-_sdp_tree_root_node)结构。 根节点包含一系列相互连接[ **SDP\_节点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdpnode/ns-sdpnode-_sdp_node)结构，其中每个包含单个 SDP 属性有关的信息。

每个 SDP\_节点结构包含[ **SDP\_节点\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdpnode/ns-sdpnode-_sdp_node_header)结构和一个[ **SDP\_节点\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdpnode/ns-sdpnode-_sdp_node_data)联合。 标头结构节点中指定包含的数据的类型。 分析驱动程序使用情况[**列表\_条目**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_list_entry)结构访问的链接可建立对等互连 SDP\_节点结构。 通过使用 SDP\_节点结构**hdr。Link.Flink**和**hdr。Link.Blink**成员，配置文件驱动程序可以获取对等节点在树中的地址。 请注意，列出\_条目指针保存到其他列表的地址\_条目结构和配置文件驱动程序必须使用[**内含\_记录**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)若要提取的地址，其中包含节点记录的宏。 有关详细信息，请参阅[ **SdpConvertStreamToTree** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthsdpddi/nc-bthsdpddi-pconvertstreamtotree)主题。

SDP 记录流转换为树表示形式后，配置文件驱动程序可以调用[ **SdpFindAttributeInTree** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpfindattributeintree)函数获取在指定节点在树中的地址。

配置文件驱动程序可以获取所有查询，本主题中所述的函数的指针[ **BTHDDI\_SDP\_分析\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_parse_interface)和[**BTHDDI\_SDP\_节点\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_node_interface)接口。 有关如何对这些接口的查询的详细信息，请参阅[蓝牙接口查询](querying-for-bluetooth-interfaces.md)。

 

 





