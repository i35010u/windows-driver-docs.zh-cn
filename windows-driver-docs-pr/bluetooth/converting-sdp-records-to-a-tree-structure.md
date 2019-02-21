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
ms.openlocfilehash: 4eb42793abbcef08fe932bf48b9632cb886243e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543097"
---
# <a name="converting-sdp-records-to-a-tree-structure"></a>将 SDP 记录转换为树状结构


服务发现协议 (SDP) 记录以复杂的二进制流进行编码。 若要启用配置文件驱动程序来分析 SDP 记录更多轻松，蓝牙驱动程序堆栈提供多个配置文件驱动程序可以使用 SDP 记录流转换为分层树形结构并切换回的函数。

客户端配置文件驱动程序可以使用[ **SdpConvertStreamToTree** ](https://msdn.microsoft.com/library/windows/hardware/ff536794)函数将 SDP 记录转换为树状结构。 调用结果的 SDP 记录的树表示形式**SdpConvertStreamToTree**函数包含一个包含与 SDP 记录关联的所有信息的根节点定义的[ **SDP\_树\_根\_节点**](https://msdn.microsoft.com/library/windows/hardware/ff536851)结构。 根节点包含一系列相互连接[ **SDP\_节点**](https://msdn.microsoft.com/library/windows/hardware/ff536848)结构，其中每个包含单个 SDP 属性有关的信息。

每个 SDP\_节点结构包含[ **SDP\_节点\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff536850)结构和一个[ **SDP\_节点\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff536849)联合。 标头结构节点中指定包含的数据的类型。 分析驱动程序使用情况[**列表\_条目**](https://msdn.microsoft.com/library/windows/hardware/ff554296)结构访问的链接可建立对等互连 SDP\_节点结构。 通过使用 SDP\_节点结构**hdr。Link.Flink**和**hdr。Link.Blink**成员，配置文件驱动程序可以获取对等节点在树中的地址。 请注意，列出\_条目指针保存到其他列表的地址\_条目结构和配置文件驱动程序必须使用[**内含\_记录**](https://msdn.microsoft.com/library/windows/hardware/ff542043)若要提取的地址，其中包含节点记录的宏。 有关详细信息，请参阅[ **SdpConvertStreamToTree** ](https://msdn.microsoft.com/library/windows/hardware/ff536794)主题。

SDP 记录流转换为树表示形式后，配置文件驱动程序可以调用[ **SdpFindAttributeInTree** ](https://msdn.microsoft.com/library/windows/hardware/ff536838)函数获取在指定节点在树中的地址。

配置文件驱动程序可以获取所有查询，本主题中所述的函数的指针[ **BTHDDI\_SDP\_分析\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff536636)和[**BTHDDI\_SDP\_节点\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff536635)接口。 有关如何对这些接口的查询的详细信息，请参阅[蓝牙接口查询](querying-for-bluetooth-interfaces.md)。

 

 





