---
title: 生成 SDP 记录
description: 生成 SDP 记录
keywords:
- 蓝牙 WDK、SDP 服务器通信
- SDP WDK 蓝牙
- 服务发现协议 WDK 蓝牙
- 浏览服务 WDK 蓝牙
- 搜索服务 WDK 蓝牙
- 服务浏览 WDK 蓝牙
- 广告服务 WDK 蓝牙
- 服务广告 WDK 蓝牙
- SdpCreateNodeTree
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6214af558ee78196c5ae22798bddc3e3faf4af95
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784221"
---
# <a name="building-sdp-records"></a>生成 SDP 记录


播发其服务的配置文件驱动程序可以从头开始构建服务发现协议 (SDP) 树层次结构，然后将它们转换为 SDP 记录流。 配置文件驱动程序必须先调用 [**SdpCreateNodeTree**](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodetree) 函数。 **SdpCreateNodeTree** 函数返回配置文件驱动程序可以使用以下函数填充的已分配和空的 [**SDP \_ 树根 \_ \_ 节点**](/windows-hardware/drivers/ddi/sdpnode/ns-sdpnode-_sdp_tree_root_node)结构：

[**SdpAddAttributeToTree**](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpaddattributetotree)

[**SdpAppendNodeToContainerNode**](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpappendnodetocontainernode)

[**SdpCreateNodeAlternative**](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodealternative)

[**SdpCreateNodeBoolean**](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeboolean)

[**SdpCreateNodeInt128**](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeint128)

[**SdpCreateNodeInt16**](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeint16)

[**SdpCreateNodeInt32**](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeint32)

[**SdpCreateNodeInt64**](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeint64)

[**SdpCreateNodeInt8**](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeint8)

[**SdpCreateNodeNil**](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodenil)

[**SdpCreateNodeSequence**](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodesequence)

[**SdpCreateNodeString**](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodestring)

[**SdpCreateNodeUInt128**](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuint128)

[**SdpCreateNodeUInt16**](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuint16)

[**SdpCreateNodeUInt32**](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuint32)

[**SdpCreateNodeUInt64**](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuint64)

[**SdpCreateNodeUInt8**](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuint8)

[**SdpCreateNodeUrl**](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeurl)

[**SdpCreateNodeUUID128**](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuuid128)

[**SdpCreateNodeUUID16**](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuuid16)

[**SdpCreateNodeUUID32**](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuuid32)

在配置文件驱动程序完成构建基于树的 SDP 记录后，它将调用 [**SdpConvertTreeToStream**](/windows-hardware/drivers/ddi/bthsdpddi/nc-bthsdpddi-pconverttreetostream) 函数来生成 SDP 记录的原始字节流版本。 在此窗体中，SDP 记录已准备就绪，可供配置文件驱动程序将其发布到本地 SDP 服务器。 与将 SDP 记录构建为流相比，此过程更方便于配置文件驱动程序使用。

**SdpConvertTreeToStream** 函数分配所需的内存来存储 SDP 记录的流版本。 当配置文件驱动程序不再需要 SDP 记录时，它必须使用 [**ExFreePool**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)释放内存。

此外，当配置文件驱动程序不再需要基于树的 SDP 记录版本时，它必须调用 [**SdpFreeTree**](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpfreetree) 来释放使用关联的 sdp \_ 树根 \_ 节点结构分配的内存 \_ 。

配置文件驱动程序可以通过查询 [**BTHDDI \_ sdp \_ 分析 \_ 接口**](/windows-hardware/drivers/ddi/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_parse_interface) 和 [**BTHDDI \_ sdp \_ 节点 \_ 接口**](/windows-hardware/drivers/ddi/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_node_interface) 接口，来获取本主题中讨论的所有函数的指针。 有关如何查询这些接口的详细信息，请参阅 [查询蓝牙接口](querying-for-bluetooth-interfaces.md)。

 

