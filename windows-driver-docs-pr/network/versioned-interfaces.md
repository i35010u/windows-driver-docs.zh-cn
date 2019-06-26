---
title: 版本受控的接口
description: 版本受控的接口
ms.assetid: 9512bfff-9225-45a3-b8c3-73469a1fe870
keywords:
- NDIS WDK、 版本控制
- 版本控制 WDK 网络
- NDIS WDK，向后兼容性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 479bb9855b6a6495c1524b2075458205346b1024
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384366"
---
# <a name="versioned-interfaces"></a>版本受控的接口





NDIS 6.0 支持版本控制的密钥结构。 此外，许多以前函数参数会移到结构。 将函数参数移动到版本控制结构允许在更高版本的 NDIS 版本中进行更改，而无需更改函数接口函数参数。

版本控制结构包含标头，指定的结构版本。 如果更改了函数参数或其他结构成员的集，该结构和其版本会更新。

此版本控制简化了向后兼容性，并扩展 NDIS 6.0 和更高版本的驱动程序的生命周期。 此外，NDIS 驱动程序可以支持多个的 NDIS 版本。

有关详细信息，请参阅[ **NDIS\_对象\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_object_header)。

 

 





