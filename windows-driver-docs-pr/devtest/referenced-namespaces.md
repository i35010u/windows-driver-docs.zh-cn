---
title: 参考的命名空间
description: 参考的命名空间
ms.assetid: 4adb0979-1e97-4697-bd85-c808023ce43f
keywords:
- WSDBIT 工具 WDK，命名空间
- WSDAPI 基本互操作性工具 WDK，命名空间
- 命名空间 WDK WSDBIT
- DWPS WDK
- Web 服务 WDK 的设备配置文件
ms.date: 05/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: f0a4d1eaadc23688306b4c6abb806f6e0c4515f6
ms.sourcegitcommit: e2de6b9ffb5c7356deb864f9da879533f49b25bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/03/2020
ms.locfileid: "91702660"
---
# <a name="referenced-namespaces"></a>参考的命名空间

下表中的信息介绍了本部分中引用的命名空间和 DWPS 规范。

>[!NOTE]
>此表中列出的命名空间前缀用于互操作性方案指南中，但不在语义上相关。

|前缀|命名空间|规范|
|----|----|----|
|soap|[https://www.w3.org/2003/05/soap-envelope](https://www.w3.org/2003/05/soap-envelope/)|SOAP 1.2 [第1部分](https://www.w3.org/TR/2003/REC-soap12-part1-20030624/) 和 [第2部分](https://www.w3.org/TR/2003/REC-soap12-part2-20030624/)|
|wsa|[http://schemas.xmlsoap.org/ws/2004/08/addressing](http://schemas.xmlsoap.org/ws/2004/08/addressing/)|[Web 服务寻址](https://www.w3.org/Submission/2004/SUBM-ws-addressing-20040810/) (ws-addressing) |
|关于|[http://schemas.xmlsoap.org/ws/2005/04/discovery](http://schemas.xmlsoap.org/ws/2005/04/discovery/)|[Web 服务发现](https://specs.xmlsoap.org/ws/2005/04/discovery/ws-discovery.pdf) (ws-management) |
|wsdp|[http://schemas.xmlsoap.org/ws/2006/02/devprof](http://schemas.xmlsoap.org/ws/2006/02/devprof/)|[设备配置文件](http://specs.xmlsoap.org/ws/2006/02/devprof/DevicesProfile.pdf)|
|wse|[http://schemas.xmlsoap.org/ws/2004/08/eventing](http://schemas.xmlsoap.org/ws/2004/08/eventing/)|[Web 服务事件](/previous-versions/ms951233(v=msdn.10)) (WS 事件) |
|wsx|[http://schemas.xmlsoap.org/ws/2004/09/mex](http://schemas.xmlsoap.org/ws/2004/09/mex/)|[Web 服务 ws-metadataexchange](http://specs.xmlsoap.org/ws/2004/09/mex/WS-MetadataExchange0904.pdf) (ws-metadataexchange) |
|.wsf|[http://schemas.xmlsoap.org/ws/2004/09/transfer](http://schemas.xmlsoap.org/ws/2004/09/transfer/)|[Web 服务传输](http://schemas.xmlsoap.org/ws/2004/09/transfer/) (WS 传输) |
|xs|[https://www.w3.org/2001/XMLSchema](https://www.w3.org/2001/XMLSchema)|[XML 架构第1部分](https://www.w3.org/TR/2001/REC-xmlschema-1-20010502/) 和 [第2部分](https://www.w3.org/TR/2001/REC-xmlschema-2-20010502/)|

除此之外， [SOAP 消息传输优化机制还 (使用 MTOM) ](https://www.w3.org/TR/2005/REC-soap12-mtom-20050125/) 。
