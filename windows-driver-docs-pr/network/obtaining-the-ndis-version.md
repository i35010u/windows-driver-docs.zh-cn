---
title: 获取 NDIS 版本
description: 获取 NDIS 版本
keywords:
- NDIS 版本信息 WDK，与操作系统版本
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fbdbcab03b4adcf1615dbfa7007ed0e96b41ec2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813651"
---
# <a name="obtaining-the-ndis-version"></a>获取 NDIS 版本





NDIS 版本可能与操作系统版本不同。 例如，如果使用 [**RtlGetVersion**](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlgetversion) 和 [**RtlVerifyVersionInfo**](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlverifyversioninfo) 例程获取操作系统版本，则不会获得与特定 NDIS 版本的保证关联。 因此，NDIS 驱动程序必须单独获取 NDIS 版本和操作系统版本。 NDIS 驱动程序可以通过 [**NdisGetVersion**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetversion) 函数获取 NDIS 版本。

## <a name="related-topics"></a>相关主题


[NDIS 版本概述](overview-of-ndis-versions.md)

[指定 NDIS 版本信息](specifying-ndis-version-information.md)

 

