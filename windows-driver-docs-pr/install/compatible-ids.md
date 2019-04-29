---
title: 兼容 ID
description: 兼容 ID 是 Windows 用来与设备 INF 文件匹配供应商定义的标识字符串。
ms.assetid: 3d20b43a-9e2b-4a8d-9a1a-eb9217233405
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca1396eab5f1f442f791a7bf8323771823c96079
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361159"
---
# <a name="compatible-id"></a>兼容 ID

兼容 ID 是 Windows 用来与设备 INF 文件匹配供应商定义的标识字符串。 设备可以有与它关联兼容 Id 的列表。 兼容 Id 应列入按顺序排列的适用性。 如果 Windows 找不到与设备的硬件 Id 之一相匹配的 INF 文件，它使用兼容 Id 来查找的 INF 文件。 兼容 Id 有相同的格式[硬件 Id](hardware-ids.md)。 但是，兼容 Id 是通常比硬件 Id 更通用的。

如果供应商指定的兼容驱动程序节点 ID 的 INF 文件，需确保其 INF 文件可支持与兼容 ID 匹配的所有硬件供应商

若要获取设备的兼容 Id 列表，请调用[ **IoGetDeviceProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty)与*DeviceProperty*参数设置为**DevicePropertyCompatibleID**。 此例程中检索的兼容 Id 列表很[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)值。 最大在兼容 ID 列表中，每个兼容 ID 和最后一个 NULL 终止符之后, 包括 NULL 终止符的字符数是 REGSTR_VAL_MAX_HCID_LEN。 Id 可能兼容 Id 列表中的最大数目为 64。
