---
title: MB 驱动程序模型版本控制
description: MB 驱动程序模型版本控制
ms.assetid: f5778b36-4f84-4cfe-965c-36af225ac0dc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc1cc6e06ca7feecc687f08851bc9c04edf4b5d2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207497"
---
# <a name="mb-driver-model-versioning"></a>MB 驱动程序模型版本控制


MB 驱动程序模型版本控制通过使用驱动程序模型版本和单个 OID 数据结构来完成。 这与 NDIS 1.x 中使用的版本控制相一致。

驱动程序型号版本定义了 MB 服务和 MB 微型端口驱动程序之间的接口发展。 各个 OID 版本跟踪对不同 MB 驱动程序模型版本中的 Oid 所做的更改。 也就是说，驱动程序模型版本定义一组 Oid，其中的数据结构由特定修订号标识。

与 *NDIS 规范*一致，MB 驱动程序模型的演变是 *累加*的。 也就是说，只能将新的 Oid 和新成员添加到现有的 OID 数据结构中。 这确保了 MB 服务可以支持微型端口驱动程序的向后兼容性。

**重要提示**   只有在极少数情况下，才会弃用现有的 Oid，或不在下一个版本中使用现有 OID 数据结构的成员。 如果发生这种情况，则这些更改及其对向后兼容性的影响应在有关 MB 驱动程序型号规范的较新版本的后续文档中清楚地记录。

 

此文档介绍了 MB 驱动程序型号的 Windows 8 版本。 驱动程序型号版本已增加到版本2.0。 某些 OID 修订将继续作为修订号1，而某些 OID 会更新到修订版2。 若要详细了解要用于各个 Oid 的修订版本，请参阅 [MB 数据模型](mb-data-model.md)。

本文档介绍了 MB 驱动程序型号的初始版本，因此驱动程序模型版本和单独的 OID 版本都以修订号1开头。

当驱动程序模型移到下一个版本时，其版本号将增加1。 添加到驱动程序模型中的任何新 Oid 将从修订版1开始;其数据结构已更改的任何现有 Oid 会将其相应修订版本增加1，并且任何不更改的现有 Oid 都将保留其各自的修订号。

驱动程序型号版本由 [OID \_ WWAN \_ 驱动程序 \_ cap](./oid-wwan-driver-caps.md)传达。 在 \_ \_ \_ [Mb 微型端口驱动程序初始化](mb-miniport-driver-initialization.md)期间，mb 服务将 OID WWAN 驱动程序 cap 查询请求发送到微型端口驱动程序。 各个 OID 修订号由[**NDIS \_ 对象 \_ 标头**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)结构的**修订**成员描述，该结构作为每个单独 OID 的数据结构的一部分包含。

 

