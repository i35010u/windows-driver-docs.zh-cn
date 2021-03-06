---
title: 版本受控的接口
description: 版本受控的接口
keywords:
- NDIS WDK，版本控制
- 版本 WDK 网络
- NDIS WDK，向后兼容性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 979ddc5d49474d2c14617dcedbf5b1be6999bf95
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248285"
---
# <a name="versioned-interfaces"></a>版本受控的接口





对于关键结构，NDIS 6.0 支持版本控制。 另外，许多以前的函数参数会移到结构。 将函数参数移到版本控制结构后，可以在以后的 NDIS 版本中更改函数参数，而无需更改函数接口。

版本控制结构包含指定结构版本的标头。 如果更改了函数参数集或其他结构成员，则将更新结构及其版本。

此版本控制简化了后向兼容性，并延长了 NDIS 6.0 和更高版本驱动程序的生存期。 此外，NDIS 驱动程序还可以支持多个版本的 NDIS。

有关详细信息，请参阅 [**NDIS \_ 对象 \_ 标头**](/windows-hardware/drivers/ddi/objectheader/ns-objectheader-ndis_object_header)。

 

