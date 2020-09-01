---
title: 筛选层
description: 筛选层
ms.assetid: db2fd1dc-c080-4f12-8138-7e66c74adacd
keywords:
- 筛选层 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91a19e7eedc9556acdd84dbd5366ac354fc2b1b3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217286"
---
# <a name="filtering-layer"></a>筛选层


*筛选层*是 tcp/ip 网络堆栈中的一个点，其中的网络数据被传递到[筛选器引擎](filter-engine.md)以与当前的一组筛选器匹配。 网络堆栈中的每个筛选层都由唯一的 [筛选层标识符](https://docs.microsoft.com/windows-hardware/drivers/network/filtering-layer-identifiers)标识。

将 [筛选器](filter.md) 添加到筛选器引擎后，会将其添加到将在其中筛选网络数据的指定筛选层。 特定 [数据字段](./data-field-identifiers.md) 在每个筛选层提供，以供已添加到该层的筛选器引擎的筛选器进行处理。 如果筛选器引擎将网络数据传递给 [标注](callout.md) 进行其他处理，则它会包括这些数据字段以及该筛选层上提供的任何 [元](https://docs.microsoft.com/windows-hardware/drivers/network/metadata-fields) 数据。

内核模式标注驱动程序使用的[运行时筛选层标识符](./run-time-filtering-layer-identifiers.md) (FWPS \_ *XXX*) 。 [管理筛选层标识符](./management-filtering-layer-identifiers.md) (FWPM \_ *Xxx*) 由**FWPM<em>Xxx</em> **函数使用，该函数与基本筛选引擎 (BFE) 从用户模式或内核模式进行交互 (例如， [**FwpmFilterAdd0**](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfilteradd0)) 。

FWPS 数据类型小于其 FWPM 的类型： FWPM 筛选层标识符是 Guid (128 位) ，而 FWPS 筛选层 [**标识符 (64**](/windows-hardware/drivers/ddi/igpupvdev/ns-igpupvdev-_luid) 位) 。 FWPS 数据类型的较小大小可提高系统性能，因为整数比较比实时流量的 GUID 比较快，而内核内存则更有效地处理 FWPS 类型。

 

