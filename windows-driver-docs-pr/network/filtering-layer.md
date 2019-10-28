---
title: 筛选层
description: 筛选层
ms.assetid: db2fd1dc-c080-4f12-8138-7e66c74adacd
keywords:
- 筛选层 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f31bf376e8c4f0a4137ae21fed2fc9d22724ffd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840488"
---
# <a name="filtering-layer"></a>筛选层


*筛选层*是 tcp/ip 网络堆栈中的一个点，其中的网络数据被传递到[筛选器引擎](filter-engine.md)以与当前的一组筛选器匹配。 网络堆栈中的每个筛选层都由唯一的[筛选层标识符](https://docs.microsoft.com/windows-hardware/drivers/network/filtering-layer-identifiers)标识。

将[筛选器](filter.md)添加到筛选器引擎后，会将其添加到将在其中筛选网络数据的指定筛选层。 特定[数据字段](https://docs.microsoft.com/windows-hardware/drivers/network/data-field-identifiers)在每个筛选层提供，以供已添加到该层的筛选器引擎的筛选器进行处理。 如果筛选器引擎将网络数据传递给[标注](callout.md)进行其他处理，则它会包括这些数据字段以及该筛选层上提供的任何[元](https://docs.microsoft.com/windows-hardware/drivers/network/metadata-fields)数据。

内核模式标注驱动程序使用[运行时筛选层标识符](https://docs.microsoft.com/windows-hardware/drivers/network/run-time-filtering-layer-identifiers)（FWPS\_*XXX*）。 从用户模式或内核模式（例如， [**FwpmFilterAdd0**](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfilteradd0)）与基本筛选引擎（BFE）交互的**FWPM<em>XXX</em>** 函数使用[管理筛选层标识符](https://docs.microsoft.com/windows-hardware/drivers/network/management-filtering-layer-identifiers)（FWPM\_*xxx*）。

FWPS 数据类型小于其 FWPM 的类型： FWPM 筛选层标识符是 Guid （128位），而 FWPS 筛选层标识符为[**luid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/igpupvdev/ns-igpupvdev-_luid)（64位）。 FWPS 数据类型的较小大小可提高系统性能，因为整数比较比实时流量的 GUID 比较快，而内核内存则更有效地处理 FWPS 类型。

 

 





