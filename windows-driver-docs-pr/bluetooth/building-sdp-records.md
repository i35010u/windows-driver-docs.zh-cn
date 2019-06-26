---
title: 生成 SDP 记录
description: 生成 SDP 记录
ms.assetid: ca3c0483-6193-4683-94bb-15466a8f332e
keywords:
- 蓝牙 WDK，SDP 服务器通信
- SDP WDK 蓝牙
- 服务发现协议 WDK 蓝牙
- 浏览服务 WDK 蓝牙
- 搜索服务 WDK 蓝牙
- 浏览 WDK 蓝牙的服务
- 广告服务 WDK 蓝牙
- 播发 WDK 蓝牙的服务
- SdpCreateNodeTree
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 716ea2d15fbf601a69b4c5de85c69dafcc105854
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354024"
---
# <a name="building-sdp-records"></a>生成 SDP 记录


播发其服务的配置文件驱动程序可以生成从零开始的服务发现协议 (SDP) 树层次结构，然后将其转换到 SDP 记录流。 配置文件驱动程序必须首先调用[ **SdpCreateNodeTree** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodetree)函数。 **SdpCreateNodeTree**函数返回一个已分配和空[ **SDP\_树\_根\_节点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdpnode/ns-sdpnode-_sdp_tree_root_node)结构配置文件驱动程序可以使用以下函数来填充：

[**SdpAddAttributeToTree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpaddattributetotree)

[**SdpAppendNodeToContainerNode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpappendnodetocontainernode)

[**SdpCreateNodeAlternative**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodealternative)

[**SdpCreateNodeBoolean**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeboolean)

[**SdpCreateNodeInt128**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeint128)

[**SdpCreateNodeInt16**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeint16)

[**SdpCreateNodeInt32**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeint32)

[**SdpCreateNodeInt64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeint64)

[**SdpCreateNodeInt8**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeint8)

[**SdpCreateNodeNil**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodenil)

[**SdpCreateNodeSequence**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodesequence)

[**SdpCreateNodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodestring)

[**SdpCreateNodeUInt128**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeuint128)

[**SdpCreateNodeUInt16**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeuint16)

[**SdpCreateNodeUInt32**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeuint32)

[**SdpCreateNodeUInt64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeuint64)

[**SdpCreateNodeUInt8**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeuint8)

[**SdpCreateNodeUrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeurl)

[**SdpCreateNodeUUID128**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeuuid128)

[**SdpCreateNodeUUID16**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeuuid16)

[**SdpCreateNodeUUID32**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeuuid32)

生成基于树的 SDP 记录配置文件驱动程序完毕后，它会调用[ **SdpConvertTreeToStream** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthsdpddi/nc-bthsdpddi-pconverttreetostream)函数以生成 SDP 记录的原始字节流版本。 在此窗体，SDP 记录已经准备好要将其发布到本地 SDP 服务器的配置文件驱动程序。 此过程可能会更方便的配置文件驱动程序比构造一个 SDP 记录以流的形式使用。

**SdpConvertTreeToStream**函数分配必要的内存来存储 SDP 记录的流版本。 当配置文件驱动程序不再需要 SDP 记录时，则它必须释放内存使用[ **ExFreePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool)。

此外，当配置文件驱动程序不再需要 SDP 记录的基于树的版本，它必须调用[ **SdpFreeTree** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpfreetree)可释放的内存分配带有关联 SDP\_树\_根\_节点结构。

配置文件驱动程序可以获取所有查询，本主题中所述的函数的指针[ **BTHDDI\_SDP\_分析\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_parse_interface)和[**BTHDDI\_SDP\_节点\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_node_interface)接口。 有关如何对这些接口的查询的详细信息，请参阅[蓝牙接口查询](querying-for-bluetooth-interfaces.md)。

 

 





