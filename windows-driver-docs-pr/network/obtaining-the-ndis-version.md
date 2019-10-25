---
title: 获取 NDIS 版本
description: 获取 NDIS 版本
ms.assetid: f7bbd11c-b6ec-4adb-8c42-ec438d518ed8
keywords:
- NDIS 版本信息 WDK，与操作系统版本
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec744da14872d49b7d6ac80592ff3cd02fd02209
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842169"
---
# <a name="obtaining-the-ndis-version"></a>获取 NDIS 版本





NDIS 版本可能与操作系统版本不同。 例如，如果使用[**RtlGetVersion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlgetversion)和[**RtlVerifyVersionInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlverifyversioninfo)例程获取操作系统版本，则不会获得与特定 NDIS 版本的保证关联。 因此，NDIS 驱动程序必须单独获取 NDIS 版本和操作系统版本。 NDIS 驱动程序可以通过[**NdisGetVersion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetversion)函数获取 NDIS 版本。

## <a name="related-topics"></a>相关主题


[NDIS 版本概述](overview-of-ndis-versions.md)

[指定 NDIS 版本信息](specifying-ndis-version-information.md)

 

 






