---
title: 在 NDIS 6.20 超过 64 个处理器的支持
description: 在 NDIS 6.20 超过 64 个处理器的支持
ms.assetid: 3fb2a09c-e2dd-48b8-a631-3793bd023ef0
keywords:
- NDIS 6.20 WDK，对超过 64 个处理器的支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebeb4656b3ad69370d7da6899d8ac1f113b8a986
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542592"
---
# <a name="support-for-more-than-64-processors-in-ndis-620"></a>在 NDIS 6.20 超过 64 个处理器的支持





NDIS 6.20 接口引入了多个 64 位处理器的支持。 早期 NDIS 版本仅限于不超过 64 个处理器 (在 x86 的 32 版本的操作系统)。

为了保持向后兼容旧实现 NDIS 支持处理器组。 未更新以支持超过 64 个处理器的软件可以默认为处理器组零。

若要支持超过 64 个处理器，NDIS 6.20 和更高版本提供了这些接口的更新的版本：

-   [接收方缩放 (RSS)](ndis-receive-side-scaling2.md)

-   处理器信息设备驱动程序接口 (请参阅[NDIS 系统信息函数](https://msdn.microsoft.com/library/windows/hardware/ff564816))

-   资源分配 (请参阅[NDIS 内存管理界面](https://msdn.microsoft.com/library/windows/hardware/ff564749))

-   读取和写锁 (请参阅[NDIS 读写锁引用](https://msdn.microsoft.com/library/windows/hardware/ff564797))

NDIS 设备驱动程序界面元素的某些已过时的 NDIS 6.20 和更高版本的驱动程序。 有关已过时的接口的详细信息，请参阅[NDIS 6.20 中已过时接口](obsolete-interfaces-in-ndis-6-20.md)。

 

 





