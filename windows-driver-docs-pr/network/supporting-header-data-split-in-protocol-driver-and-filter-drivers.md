---
title: 支持标头数据拆分为协议和筛选器驱动程序
description: 支持协议驱动程序和筛选器驱动程序中的标头数据拆分
ms.assetid: ba1566f2-7da6-4472-b00b-e25bf7acc294
keywords:
- 标头数据拆分 WDK，协议驱动程序
- 标头数据拆分 WDK，筛选器驱动程序
- 协议驱动程序 WDK 网络，标头数据拆分
- 筛选器驱动程序 WDK 网络，标头数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49de6937aea5f5cfa53adddf33c41f56b67494e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569466"
---
# <a name="supporting-header-data-split-in-protocol-drivers-and-filter-drivers"></a>支持协议驱动程序和筛选器驱动程序中的标头数据拆分





NDIS 6.0 和更高版本的协议驱动程序和筛选器驱动程序必须支持不连续的缓冲区中接收与标头和数据的指示。

您必须假定是仅在单个 MDL [ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构。 协议驱动程序和筛选器驱动程序不需要执行任何操作特定于支持标头数据拆分注册。 但该驱动程序收到处理代码必须处理多个 MDL MDL 链中的，必须使用以下 NDIS MDL 宏来访问 MDL 链：

-   [**NET\_BUFFER\_FIRST\_MDL**](https://msdn.microsoft.com/library/windows/hardware/ff568386)

-   [**NET\_BUFFER\_CURRENT\_MDL**](https://msdn.microsoft.com/library/windows/hardware/ff568379)

-   [**NET\_BUFFER\_CURRENT\_MDL\_OFFSET**](https://msdn.microsoft.com/library/windows/hardware/ff568380)

拆分缓冲的数据长度与该键相关联 NET\_缓冲区结构 (在**DataLength**的成员[ **NET\_缓冲区\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff568381)结构) 跨多个 MDLs 拆分。 例如，如果尝试访问整个数据缓冲区中的第一个 MDL 协议驱动程序，该驱动程序无法访问无效数据。

**请注意**  微型端口驱动程序接收指示调用将返回到微型端口驱动程序后，可以回收 MDLs 的标头。 基础驱动程序或其客户端必须接收指示调用返回微型端口驱动程序之后访问的标头 MDLs。 此限制也适用甚至当微型端口驱动程序不指示接收到的数据与的 NDIS 状态\_接收\_标志\_资源。

 

 

 





