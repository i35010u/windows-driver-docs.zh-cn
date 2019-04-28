---
title: MB 驱动程序模型版本控制
description: MB 驱动程序模型版本控制
ms.assetid: f5778b36-4f84-4cfe-965c-36af225ac0dc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b72b67507864b2177cd42ae43c318da390cf0ea7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343374"
---
# <a name="mb-driver-model-versioning"></a>MB 驱动程序模型版本控制


MB 驱动程序模型版本控制的驱动程序模型版本和单个 OID 数据结构修订，从而实现同步。 这与在 NDIS 中使用的版本控制模式是一致 6.x。

驱动程序模型版本定义 MB 服务和 MB 微型端口驱动程序之间的接口演变。 各个 OID 修订跟踪的 Oid 不同 MB 驱动程序模型版本中所做的更改。 也就是说，驱动程序模型版本定义一组由特定的修订号标识的数据结构的 Oid。

与一致*NDIS 规范*，是 MB 驱动程序模型演变*累加性*。 也就是说，新 Oid 和新的成员只能添加到现有的 OID 数据结构。 这可确保 MB 服务可以支持的微型端口驱动程序的向后兼容性。

**重要**  只有在极少数情况下将现有的 Oid 不推荐使用或的现有 OID 数据结构的成员不能在下一版本。 如果发生这种情况，这些更改，并且它们在向后兼容性的影响应清楚地记录有关 MB 驱动程序模型规范的较新版本的后续文档中。

 

本文档介绍了 Windows 8 版本的 MB 驱动程序模型。 驱动程序模型版本递增到版本 2.0。 某些 OID 修订继续修订号 1，而一些具有已更新到版本 2。 有关使用各自的 Oid 的修订版本的详细信息，请参阅[MB 数据模型](mb-data-model.md)。

本文档介绍了 MB 驱动程序模型的初始版本，因此驱动程序模型版本和各个 OID 修订的修订数字 1 开头。

当驱动程序模型移动到下一个版本时，其版本号将增加 1。 添加到驱动程序模型中任何新 Oid 将开始修订版 1;结构已更改其数据在其相应的修订版本将增加 1，任何现有 Oid 并不会更改任何现有 Oid 将保留其各自的修订号。

驱动程序模型版本所传达[OID\_WWAN\_驱动程序\_CAPS](https://msdn.microsoft.com/library/windows/hardware/ff569825)。 MB 服务发送一个 OID\_WWAN\_驱动程序\_CAPS 查询请求期间的微型端口驱动程序[MB 微型端口驱动程序初始化](mb-miniport-driver-initialization.md)。 由描述各个 OID 修订**修订**的成员[ **NDIS\_对象\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff566588)结构，它是作为一部分包含每个单个 OID 的数据结构。

 

 





