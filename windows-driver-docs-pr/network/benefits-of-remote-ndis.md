---
title: 远程 NDIS 的优势
description: 远程 NDIS 的优势
keywords:
- 远程 NDIS WDK 网络，优点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98d1cda70fc386da81504ce03ca6b7eb8169f6b0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817655"
---
# <a name="benefits-of-remote-ndis"></a>远程 NDIS 的优势





远程 NDIS 是理解并经过时间考验的 NDIS 体系结构的扩展。 NDIS 为特定于设备的 NDIS 微型端口驱动程序定义函数调用接口。 此接口定义用于发送和接收网络数据的基元，并用于查询和设置配置参数和统计信息。 远程 NDIS 通过为 NDIS 微型端口驱动程序接口定义消息包装来利用 NDIS，从而将 NDIS 处理代码从微型端口驱动程序移动到设备本身。 通过此方法和其他方式，远程 NDIS 允许各种设备功能和性能级别。 远程 NDIS 模型有许多优点：

-   扩展性，无需更改到特定于总线的消息传输机制

-   能够在更短的时间内通过更多的总线支持更多的协议

-   已为网络和外部总线设备型号经过证实的驱动程序体系结构

对于远程 NDIS 设备，支持 NDIS 网络堆栈中已经存在的增值机制。

 

 





