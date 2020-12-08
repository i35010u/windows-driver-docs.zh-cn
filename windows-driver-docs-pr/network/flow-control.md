---
title: 流控制
description: 流控制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e327a66d3883b4337b113225769f018830f1e8d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786175"
---
# <a name="flow-control"></a>流控制





Usb 远程 NDIS 设备的流控制由 USB 规范定义。

由于 USB 上的所有通信都基于主机到设备的事务，因此，所有主机都必须执行此操作，以使数据流停止向大容量管道上的设备发出令牌。 如果设备需要断言流控制，则应 NAK 从主机进行数据传输，直到它能够再次处理数据。 有关此过程的详细说明，请参阅 dbms-guide-8.4.4 中的 "USB 规范版本 1.1" 部分。

 

 





