---
title: 常见控制节点和筛选器
description: 常见控制节点和筛选器
ms.assetid: 33e0605b-0fd1-4506-a48b-427976e94dfc
keywords:
- 控制节点 WDK BDA
- 节点 WDK BDA
- 网络提供商筛选 WDK BDA
- 调谐器控制节点 WDK BDA
- 解调器控制节点 WDK BDA
- 捕获筛选器 WDK BDA
- PID 筛选器控制节点 WDK BDA
- IPSink WDK BDA
- NDISIP WDK BDA
- 广播驱动程序体系结构 WDK AVStream，控制节点
- BDA WDK AVStream，控制节点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5548cbfb31875ed0c5cdad67b1895ce00a87124e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329738"
---
# <a name="common-control-nodes-and-filters"></a>常见控制节点和筛选器





控制节点和在各图所示的筛选器的类型[控制节点、 筛选器和硬件](control-nodes--filters-and-hardware.md)部分共有的数字地面，卫星接收并连接好电缆广播。 但是，可以创建其他节点类型和各种广播的媒体和设备的筛选器。 请务必记住每个控制节点需要不对应单个 BDA 设备筛选器。 在某些情况下，单个 BDA 设备筛选器可以封装多个控制节点。

以下列表描述控制节点和广播体系结构中的筛选器：

<a href="" id="network-provider"></a>**网络提供商**  
一个*网络提供程序筛选器*(或*网络提供商*) 通过 BDA 设备会路由到数字电视信号。 各种广播提供程序当前通过三种基本的网络类型-附属、 电缆和天线传输数字电视信号。 这些数字信号进行传输中所定义的多个标准，包括 ATSC、 DVB-S、 DVB C 和 DVB-T。 格式 BDA 设备接收和管理这些数字信号。

网络提供商：

-   虽然没有数据实际上将通过此模块是筛选器关系图，源筛选器。

-   为每个网络类型存在，或者可创建的新的网络类型。

-   参与了关系图构建过程。

-   与通过属性和方法初始化此类筛选器的 BDA 微型驱动程序组关系图中的其他筛选器进行通信。

每个网络提供程序可以生成不同的图形配置其关联的网络类型。 应用程序将请求调整传递到网络提供程序，后者又将信息传递到 BDA 微型驱动程序。 请参阅 Microsoft Windows SDK 文档了解详细信息的广播体系结构部分。

<a href="" id="tuner"></a>**调谐器**  
此控制节点筛选携带传输流的特定频率。 它可以独自或与其他控件节点，在筛选器内显示。

<a href="" id="demodulator"></a>**解调器**  
模拟信号转换为数字位流控制节点。 它可以独自或与其他控件节点，在筛选器内显示。

<a href="" id="capture"></a>**捕获**  
将数据移到主机内存中一个筛选器。

<a href="" id="pid-filter"></a>**PID 筛选器**  
将从传输流中选择一个或多个基本数据库流控制节点。 这是信号分离器的主要功能。 它可以独自或与其他控件节点，在筛选器内显示。

<a href="" id="mpe-parser"></a>**MPE 分析器**  
分析包含 mpeg-2 专用部分的流中的 IP 数据筛选器。

<a href="" id="ipsink"></a>**IPSink**  
数据示例并将数据转发到 NDIS TCP/IP 堆栈接受 IP 数据包筛选器。

<a href="" id="ndisip"></a>**NDISIP**  
充当 IPSink 筛选器传递的数据的网络适配器的接收方 NDIS 微型端口驱动程序。

**请注意**  从 Windows Vista 开始，不支持 IPSink 筛选器。

 

 

 




