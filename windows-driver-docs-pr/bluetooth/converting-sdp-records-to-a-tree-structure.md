---
title: 将 SDP 记录转换为树状结构
description: 将 SDP 记录转换为树状结构
ms.assetid: 762cf68b-0082-4b9e-8f24-ff19ecf6f8bd
keywords:
- 蓝牙 WDK、SDP 服务器通信
- SDP WDK 蓝牙
- 服务发现协议 WDK 蓝牙
- 浏览服务 WDK 蓝牙
- 搜索服务 WDK 蓝牙
- 服务浏览 WDK 蓝牙
- 转换 SDP 记录
- 来自 SDP 的树结构记录 WDK 蓝牙
- SdpConvertStreamToTree
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfea61df8d5f8561f42b9411176528326331df9e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833872"
---
# <a name="converting-sdp-records-to-a-tree-structure"></a>将 SDP 记录转换为树状结构


服务发现协议（SDP）记录在复杂的二进制流中进行编码。 为了使配置文件驱动程序能够更轻松地分析 SDP 记录，蓝牙驱动程序堆栈提供了许多功能，配置文件驱动程序可以使用这些功能将 SDP 记录流转换为分层树结构并再次返回。

客户端配置文件驱动程序可以使用[**SdpConvertStreamToTree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthsdpddi/nc-bthsdpddi-pconvertstreamtotree)函数将 SDP 记录转换为树结构。 通过调用**SdpConvertStreamToTree**函数而生成的 sdp 记录的树表示形式包含一个根节点，该节点包含与 sdp 记录关联的所有信息，由[**sdp\_树\_根定义\_节点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdpnode/ns-sdpnode-_sdp_tree_root_node)结构。 根节点包含一系列互连的[**SDP\_节点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdpnode/ns-sdpnode-_sdp_node)结构，其中每个都包含一个 SDP 属性的相关信息。

每个 SDP\_节点结构包含一个[**sdp\_节点\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdpnode/ns-sdpnode-_sdp_node_header)结构和一个[**sdp\_节点\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdpnode/ns-sdpnode-_sdp_node_data)联合。 标头结构指定节点中包含的数据的类型。 配置文件驱动程序使用[**LIST\_条目**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_list_entry)结构来访问对等 SDP\_节点结构的链接。 使用 SDP\_节点结构的**hdr。Flink**和**hdr。链接。闪烁**成员，配置文件驱动程序可以获取树中对等节点的地址。 请记住，LIST\_项指针会将地址保存到其他列表\_条目结构，而配置文件驱动程序必须使用[**包含\_record**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)宏来提取包含节点记录的地址。 有关详细信息，请参阅[**SdpConvertStreamToTree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthsdpddi/nc-bthsdpddi-pconvertstreamtotree)主题。

将 SDP 记录流转换为树表示形式后，配置文件驱动程序可以调用[**SdpFindAttributeInTree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpfindattributeintree)函数以获取树中指定节点的地址。

配置文件驱动程序可以通过查询[**BTHDDI\_SDP\_PARSE\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_parse_interface)和[**BTHDDI\_SDP\_节点\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_node_interface)接口，来获取本主题中讨论的所有函数的指针。 有关如何查询这些接口的详细信息，请参阅[查询蓝牙接口](querying-for-bluetooth-interfaces.md)。

 

 





