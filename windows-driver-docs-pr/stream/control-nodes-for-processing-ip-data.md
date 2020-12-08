---
title: 用于处理 IP 数据的控制节点
description: 用于处理 IP 数据的控制节点
keywords:
- 控制节点 WDK BDA
- 节点 WDK BDA
- IP 数据处理 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: debbe55e494dac19f14586de13915b6bd8828ad1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817977"
---
# <a name="control-nodes-for-processing-ip-data"></a>用于处理 IP 数据的控制节点





以下顺序和图描述了收到的数字信号中的 IP 数据的数据流。

1.  接收方设备接收 IP 数据，并在传输流中通过 PC 总线传递 IP 数据。

2.  信号分离器接收传输流并传递包含 IP 数据的专用部分。

3.  专用部分由多协议封装 (MPE) 分析器接收，这将删除多协议封装并输出 IP 数据。 MPE 分析器将 IP 数据传递到 IPSink 筛选器。

4.  IPSink 筛选器通过专用接口将 IP 数据传递到广播 NDISIP 微型端口驱动程序。

5.  NDISIP 微型端口驱动程序作为虚拟 NDIS 小型端口安装。 NDISIP 微型端口驱动程序将 IP 数据发送到 NDIS。

6.  NDIS 通过 TCP/IP 和 Windows 套接字 (WinSock) 传播 IP 数据，就像对任何其他 NDIS 适配器一样。

**注意**   从 Windows Vista 开始，不支持 IPSink 筛选器。

 

![说明 ip 数据流的图示](images/ipdata.png)

 

 




