---
title: 生成 SDP 记录
description: 生成 SDP 记录
ms.assetid: ca3c0483-6193-4683-94bb-15466a8f332e
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
ms.openlocfilehash: 217e63ec512fe88797b4794cdffa83b759998774
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832126"
---
# <a name="building-sdp-records"></a>生成 SDP 记录


通告其服务的配置文件驱动程序可以从头开始构建服务发现协议（SDP）树层次结构，然后将其转换为 SDP 记录流。 配置文件驱动程序必须先调用[**SdpCreateNodeTree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodetree)函数。 **SdpCreateNodeTree**函数返回已分配的空[**SDP\_树\_根\_节点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdpnode/ns-sdpnode-_sdp_tree_root_node)结构，配置文件驱动程序可以使用以下函数填充该结构：

[**SdpAddAttributeToTree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpaddattributetotree)

[**SdpAppendNodeToContainerNode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpappendnodetocontainernode)

[**SdpCreateNodeAlternative**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodealternative)

[**SdpCreateNodeBoolean**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeboolean)

[**SdpCreateNodeInt128**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeint128)

[**SdpCreateNodeInt16**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeint16)

[**SdpCreateNodeInt32**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeint32)

[**SdpCreateNodeInt64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeint64)

[**SdpCreateNodeInt8**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeint8)

[**SdpCreateNodeNil**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodenil)

[**SdpCreateNodeSequence**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodesequence)

[**SdpCreateNodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodestring)

[**SdpCreateNodeUInt128**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuint128)

[**SdpCreateNodeUInt16**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuint16)

[**SdpCreateNodeUInt32**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuint32)

[**SdpCreateNodeUInt64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuint64)

[**SdpCreateNodeUInt8**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuint8)

[**SdpCreateNodeUrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeurl)

[**SdpCreateNodeUUID128**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuuid128)

[**SdpCreateNodeUUID16**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuuid16)

[**SdpCreateNodeUUID32**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuuid32)

在配置文件驱动程序完成构建基于树的 SDP 记录后，它将调用[**SdpConvertTreeToStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthsdpddi/nc-bthsdpddi-pconverttreetostream)函数来生成 SDP 记录的原始字节流版本。 在此窗体中，SDP 记录已准备就绪，可供配置文件驱动程序将其发布到本地 SDP 服务器。 与将 SDP 记录构建为流相比，此过程更方便于配置文件驱动程序使用。

**SdpConvertTreeToStream**函数分配所需的内存来存储 SDP 记录的流版本。 当配置文件驱动程序不再需要 SDP 记录时，它必须使用[**ExFreePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)释放内存。

此外，当配置文件驱动程序不再需要基于树的 SDP 记录版本时，它必须调用[**SdpFreeTree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpfreetree)来释放使用关联的 SDP\_树分配的内存\_根\_节点结构。

配置文件驱动程序可以通过查询[**BTHDDI\_SDP\_PARSE\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_parse_interface)和[**BTHDDI\_SDP\_节点\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_node_interface)接口，来获取本主题中讨论的所有函数的指针。 有关如何查询这些接口的详细信息，请参阅[查询蓝牙接口](querying-for-bluetooth-interfaces.md)。

 

 





