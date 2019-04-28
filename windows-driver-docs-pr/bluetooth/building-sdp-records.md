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
ms.openlocfilehash: 39b49ae2fa41719fd0195dce0f5f5320d5d52c4a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328252"
---
# <a name="building-sdp-records"></a>生成 SDP 记录


播发其服务的配置文件驱动程序可以生成从零开始的服务发现协议 (SDP) 树层次结构，然后将其转换到 SDP 记录流。 配置文件驱动程序必须首先调用[ **SdpCreateNodeTree** ](https://msdn.microsoft.com/library/windows/hardware/ff536818)函数。 **SdpCreateNodeTree**函数返回一个已分配和空[ **SDP\_树\_根\_节点**](https://msdn.microsoft.com/library/windows/hardware/ff536851)结构配置文件驱动程序可以使用以下函数来填充：

[**SdpAddAttributeToTree**](https://msdn.microsoft.com/library/windows/hardware/ff536784)

[**SdpAppendNodeToContainerNode**](https://msdn.microsoft.com/library/windows/hardware/ff536786)

[**SdpCreateNodeAlternative**](https://msdn.microsoft.com/library/windows/hardware/ff536798)

[**SdpCreateNodeBoolean**](https://msdn.microsoft.com/library/windows/hardware/ff536801)

[**SdpCreateNodeInt128**](https://msdn.microsoft.com/library/windows/hardware/ff536802)

[**SdpCreateNodeInt16**](https://msdn.microsoft.com/library/windows/hardware/ff536804)

[**SdpCreateNodeInt32**](https://msdn.microsoft.com/library/windows/hardware/ff536806)

[**SdpCreateNodeInt64**](https://msdn.microsoft.com/library/windows/hardware/ff536808)

[**SdpCreateNodeInt8**](https://msdn.microsoft.com/library/windows/hardware/ff536811)

[**SdpCreateNodeNil**](https://msdn.microsoft.com/library/windows/hardware/ff536812)

[**SdpCreateNodeSequence**](https://msdn.microsoft.com/library/windows/hardware/ff536814)

[**SdpCreateNodeString**](https://msdn.microsoft.com/library/windows/hardware/ff536816)

[**SdpCreateNodeUInt128**](https://msdn.microsoft.com/library/windows/hardware/ff536819)

[**SdpCreateNodeUInt16**](https://msdn.microsoft.com/library/windows/hardware/ff536822)

[**SdpCreateNodeUInt32**](https://msdn.microsoft.com/library/windows/hardware/ff536824)

[**SdpCreateNodeUInt64**](https://msdn.microsoft.com/library/windows/hardware/ff536827)

[**SdpCreateNodeUInt8**](https://msdn.microsoft.com/library/windows/hardware/ff536828)

[**SdpCreateNodeUrl**](https://msdn.microsoft.com/library/windows/hardware/ff536831)

[**SdpCreateNodeUUID128**](https://msdn.microsoft.com/library/windows/hardware/ff536833)

[**SdpCreateNodeUUID16**](https://msdn.microsoft.com/library/windows/hardware/ff536835)

[**SdpCreateNodeUUID32**](https://msdn.microsoft.com/library/windows/hardware/ff536836)

生成基于树的 SDP 记录配置文件驱动程序完毕后，它会调用[ **SdpConvertTreeToStream** ](https://msdn.microsoft.com/library/windows/hardware/ff536796)函数以生成 SDP 记录的原始字节流版本。 在此窗体，SDP 记录已经准备好要将其发布到本地 SDP 服务器的配置文件驱动程序。 此过程可能会更方便的配置文件驱动程序比构造一个 SDP 记录以流的形式使用。

**SdpConvertTreeToStream**函数分配必要的内存来存储 SDP 记录的流版本。 当配置文件驱动程序不再需要 SDP 记录时，则它必须释放内存使用[ **ExFreePool**](https://msdn.microsoft.com/library/windows/hardware/ff544590)。

此外，当配置文件驱动程序不再需要 SDP 记录的基于树的版本，它必须调用[ **SdpFreeTree** ](https://msdn.microsoft.com/library/windows/hardware/ff536839)可释放的内存分配带有关联 SDP\_树\_根\_节点结构。

配置文件驱动程序可以获取所有查询，本主题中所述的函数的指针[ **BTHDDI\_SDP\_分析\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff536636)和[**BTHDDI\_SDP\_节点\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff536635)接口。 有关如何对这些接口的查询的详细信息，请参阅[蓝牙接口查询](querying-for-bluetooth-interfaces.md)。

 

 





