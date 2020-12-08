---
title: 常见控制节点和筛选器
description: 常见控制节点和筛选器
keywords:
- 控制节点 WDK BDA
- 节点 WDK BDA
- 网络提供程序筛选 WDK BDA
- 调谐器控制节点 WDK BDA
- 解调器控制节点 WDK BDA
- 捕获筛选器 WDK BDA
- PID 筛选器控件节点 WDK BDA
- IPSink WDK BDA
- NDISIP WDK BDA
- 广播驱动程序体系结构 WDK AVStream，控制节点
- BDA WDK AVStream，控制节点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1353dfe2c7b8c113ec40ca15a3162dae05290fce
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785477"
---
# <a name="common-control-nodes-and-filters"></a>常见控制节点和筛选器





" [控制节点"、"筛选器和硬件](control-nodes--filters-and-hardware.md) " 部分的图中显示的控制节点和筛选器的类型是接收数字卫星、地面和电缆广播的常见情况。 不过，你也可以为各种广播媒体和设备创建其他节点类型和筛选器。 务必记住，每个控制节点不需要对应于单个 BDA 设备筛选器。 在某些情况下，单个 BDA 设备筛选器可以封装多个控制节点。

以下列表描述了在广播体系结构中常见的控制节点和筛选器：

<a href="" id="network-provider"></a>**网络提供商**  
*网络提供商筛选器* (或 *网络提供商*) 将数字电视信号发送到 BDA 设备并通过该设备路由。 各种广播提供商当前在三种基本网络类型（卫星、电缆和天线）上传输数字电视信号。 这些数字信号以多种标准（包括 ATSC、DVB-T、DVB-T 和 DVB-T）定义的格式传输。 BDA 设备接收并管理这些数字信号。

网络提供商：

-   是筛选器图中的源筛选器，但实际上没有数据通过它。

-   对于每个网络类型都存在或可为新的网络类型创建。

-   参与图形构建过程。

-   通过微型驱动程序初始化此类筛选器的属性和方法集，与图形中的其他筛选器通信。

每个网络提供程序可以为其关联的网络类型构建不同的图形配置。 应用程序将微调请求传递到网络提供程序，而网络提供程序会将信息传递到 BDA 微型驱动程序。 有关详细信息，请参阅 Microsoft Windows SDK 文档的广播体系结构部分。

<a href="" id="tuner"></a>**式**  
此控制节点对携带传输流的特定频率进行筛选。 它可以单独显示在筛选器内部，也可以与其他控件节点一起出现。

<a href="" id="demodulator"></a>**解调器**  
一个控制节点，它将模拟信号转换为数字位流。 它可以单独显示在筛选器内部，也可以与其他控件节点一起出现。

<a href="" id="capture"></a>**抓住**  
将数据移入主机内存的筛选器。

<a href="" id="pid-filter"></a>**PID 筛选器**  
一个控制节点，该节点从传输流中选择一个或多个基本数据流。 这是一个信号分离器的主要功能。 它可以单独显示在筛选器内部，也可以与其他控件节点一起出现。

<a href="" id="mpe-parser"></a>**MPE 分析器**  
一种筛选器，它从包含 MPEG-2 专用部分的流分析 IP 数据。

<a href="" id="ipsink"></a>**IPSink**  
接受 IP 数据包作为数据采样并将数据转发到 NDIS TCP/IP 堆栈的筛选器。

<a href="" id="ndisip"></a>**NDISIP**  
一种 NDIS 微型端口驱动程序，充当网络适配器接收方，用于 IPSink 筛选器所通过的数据。

**注意**   从 Windows Vista 开始，不支持 IPSink 筛选器。

 

 

 




