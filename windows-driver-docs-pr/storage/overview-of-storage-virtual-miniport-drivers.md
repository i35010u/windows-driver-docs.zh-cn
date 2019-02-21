---
title: 存储虚拟微型端口驱动程序的概述
description: 存储虚拟微型端口驱动程序的概述
ms.assetid: 5aee56e6-610c-4718-8566-9285682049cb
keywords:
- 存储虚拟微型端口驱动程序 WDK，关于
- 虚拟微型端口驱动程序 WDK
- 微型端口驱动程序 WDK 存储虚拟
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66912362b0e66c6938ab804e8e09d5bb8cc209d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524314"
---
# <a name="overview-of-storage-virtual-miniport-drivers"></a>存储虚拟微型端口驱动程序的概述


若要扩展的 Windows Vista Service Pack 1 (SP1) 和 Windows Server 2008 Storport 接口的用途，Microsoft 还定义了虚拟微型端口 (VMiniport) 驱动程序接口。 此接口可用于当前具有严格无意将它们与物理硬件的微型端口驱动程序。 这些更改并删除对硬件关联 （"物理"） 微型端口驱动程序来调用仅 Storport 例程的限制。 与物理微型端口驱动程序，不同虚拟微型端口驱动程序可以进行 WDM 的文档所述对 Windows 驱动程序模型 (WDM) 例程的调用。 除非另有说明，从这一刻起术语"微型端口"将用于到"虚拟微型端口"，请参阅。

虚拟微型端口驱动程序接口释放依赖于用于处理内存和同步端口驱动程序 (Storport) 微型端口。 接口使虚拟微型端口驱动程序之前暂时不可用的方式执行 I/O。 这些更改将定向到，但不是限于将来启用存储技术 （例如 iSCSI 和 Infiniband） 和非标准的存储接口。

实现 VMiniport 驱动程序时要格外小心。 尽管扩展提供更大的灵活性，他们需要更多关注中检测错误，验证路径和 I/O 计时。 在这里，提供了一些示例，但仍不可能以应对预期的不正确地使用内核接口的所有可能的结果。

 

 




