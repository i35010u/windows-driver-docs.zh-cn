---
title: Storport 的历史记录
description: Storport 的历史记录
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8561b1bae51d8b9ebbafbb0c7e41f478aa1008d6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835159"
---
# <a name="history-of-storport"></a>Storport 的历史记录


Microsoft Windows Server 2003 和更高版本提供了 Storport (*Storport.sys*) ，这是一个特别适用于高性能总线（如光纤通道总线和 RAID 适配器）的存储端口驱动程序。

为了扩展 Storport 接口的有用性，对于带有 Service Pack 1 (SP1) 和 Windows Server 2008 的 Windows Vista，Microsoft 已定义虚拟小型端口 (VMiniport) 驱动程序接口。 此接口适用于当前与物理硬件无严格关联的微型端口驱动程序。

在 Windows 7 之前的 Storport 版本中，Storport 的系统事件日志接口为微型端口驱动程序提供了内核系统事件日志工具的一小部分功能的访问权限，这会严重影响微型端口事件日志条目的有用性。 对于 Windows 7，新的 Storport 事件日志接口允许微型端口驱动程序对 Windows 内核事件设施的功能具有完全访问权限。 这种访问可让微型端口驱动程序创建在排查存储问题时真正有用的事件日志条目。

Storport 在 Windows 系统中提供更高的性能体系结构和更好的光纤通道兼容性。

 

 




