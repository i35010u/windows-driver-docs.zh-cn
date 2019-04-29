---
title: 用于处理 IP 数据的控制节点
description: 用于处理 IP 数据的控制节点
ms.assetid: 6195ffe9-d20c-4687-8d45-abbfc17ba2fa
keywords:
- 控制节点 WDK BDA
- 节点 WDK BDA
- IP 数据处理 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74dbc450a7c83e74839cc5b35a50b66b18b246b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374199"
---
# <a name="control-nodes-for-processing-ip-data"></a>用于处理 IP 数据的控制节点





以下序列和图描述中接收到的数字信号 IP 数据的数据流。

1.  接收方设备接收 IP 数据并将 IP 数据通过 PC 总线传递作为传输流的一部分。

2.  信号分离器接收传输流，并将传递包含 IP 数据的私有部分。

3.  多协议封装 (MPE) 分析器，这将移除多协议封装并输出 IP 数据由接收的私有部分。 MPE 分析器将 IP 数据传递给 IPSink 筛选器。

4.  IPSink 筛选器将 IP 数据通过专用接口传递给广播 NDISIP 微型端口驱动程序。

5.  作为虚拟的 NDIS 微型端口安装 NDISIP 微型端口驱动程序。 NDISIP 微型端口驱动程序将 IP 数据发送到 NDIS。

6.  NDIS 传播通过 TCP/IP 和 Windows 套接字 (WinSock) 的 IP 数据，像任何其他 NDIS 适配器。

**请注意**  从 Windows Vista 开始，不支持 IPSink 筛选器。

 

![说明 ip 数据流关系图](images/ipdata.png)

 

 




