---
title: 获取 NDIS 版本
description: 获取 NDIS 版本
ms.assetid: f7bbd11c-b6ec-4adb-8c42-ec438d518ed8
keywords:
- NDIS 版本信息 WDK，与操作系统版本
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3828523ea30d891762ed3d1f7b829f0215c3c3ba
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206409"
---
# <a name="obtaining-the-ndis-version"></a>获取 NDIS 版本





NDIS 版本可能与操作系统版本不同。 例如，如果使用 [**RtlGetVersion**](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlgetversion) 和 [**RtlVerifyVersionInfo**](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlverifyversioninfo) 例程获取操作系统版本，则不会获得与特定 NDIS 版本的保证关联。 因此，NDIS 驱动程序必须单独获取 NDIS 版本和操作系统版本。 NDIS 驱动程序可以通过 [**NdisGetVersion**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetversion) 函数获取 NDIS 版本。

## <a name="related-topics"></a>相关主题


[NDIS 版本概述](overview-of-ndis-versions.md)

[指定 NDIS 版本信息](specifying-ndis-version-information.md)

 

