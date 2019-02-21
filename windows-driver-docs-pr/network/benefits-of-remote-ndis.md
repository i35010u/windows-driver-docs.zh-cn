---
title: 远程 NDIS 的优点
description: 远程 NDIS 的优点
ms.assetid: ca559f2e-c7e3-4b8e-a04d-f3a544d33a68
keywords:
- 远程 NDIS WDK 网络、 优点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 101186eaf0d6017731111d74fd02a6358f01b675
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522956"
---
# <a name="benefits-of-remote-ndis"></a>远程 NDIS 的优点





远程 NDIS 是易于理解和经过时间考验 NDIS 体系结构的扩展。 NDIS 定义特定于设备的 NDIS 微型端口驱动程序的函数调用接口。 此接口定义基元来发送和接收网络数据，并以查询和设置配置参数和统计信息。 远程 NDIS 利用 NDIS 通过定义由消息包装为 NDIS 微型端口驱动程序接口，因此将 NDIS 处理代码从微型端口驱动程序移动到设备本身。 在此环境及其他方式，远程 NDIS 允许各种设备功能和性能级别。 远程 NDIS 模型具有以下优点：

-   而无需更改的特定于总线的消息传输机制可扩展性

-   通过在短时间的多个总线支持多个协议的能力

-   已被证实的网络和外部总线的设备型号的驱动程序体系结构

远程 NDIS 设备都支持 NDIS 网络堆栈中已存在的增值机制。

 

 





