---
title: 实现 NDIS 6.40 驱动程序
description: NDIS 6.40 驱动程序必须遵循在 NDIS 6.30 驱动程序实现中定义的要求。
ms.assetid: 860DFD3E-F324-417A-A625-3C2935752DA2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43e4a15b40c941613d53090aabc508838100e3ce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562520"
---
# <a name="implementing-an-ndis-640-driver"></a>实现 NDIS 6.40 驱动程序


NDIS 6.40 驱动程序必须遵循在中定义的要求[实现 NDIS 6.30 驱动程序](implementing-an-ndis-6-30-driver.md)。

此外，NDIS 6.40 驱动程序必须符合以下要求：

-   NDIS 6.40 驱动程序必须报告正确的 NDIS 版本时它会向 NDIS 注册。

    必须更新的主版本号和次的 NDIS 版本编号在 NDIS\_*Xxx*\_驱动程序\_支持 NDIS 6.40 特征结构。 **MajorNdisVersion**成员必须包含**6**并**MinorNdisVersion**成员必须包含**40**。 此要求适用于微型端口、 协议和筛选器驱动程序。 您还必须更新的版本信息对于编译器，请参阅[编译 NDIS 6.40 驱动程序](compiling-an-ndis-6-40-driver.md)。

-   适用于 Windows 8.1 和 Windows Server 2012 R2 操作系统的 NDIS 6.40 微型端口驱动程序必须使用数据结构的 NDIS 6.40 版本。 有关详细信息，请参阅[使用 NDIS 6.40 数据结构](using-ndis-6-40-data-structures.md)。

 

 





