---
title: 获取 NDIS 版本
description: 获取 NDIS 版本
ms.assetid: f7bbd11c-b6ec-4adb-8c42-ec438d518ed8
keywords:
- 操作系统版本与的 NDIS 版本信息 WDK，
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ae668097acb96772b3918536e022613aa923dbd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354504"
---
# <a name="obtaining-the-ndis-version"></a>获取 NDIS 版本





NDIS 版本可能不会与操作系统版本相同。 例如，如果您使用[ **RtlGetVersion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlgetversion)并[ **RtlVerifyVersionInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlverifyversioninfo)例程，从而获取操作系统版本中，执行操作获取与特定的 NDIS 版本的有保证的关联。 因此，NDIS 驱动程序必须获得 NDIS 版本和操作系统版本单独。 NDIS 驱动程序可以获取与的 NDIS 版本[ **NdisGetVersion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisgetversion)函数。

## <a name="related-topics"></a>相关主题


[NDIS 版本的概述](overview-of-ndis-versions.md)

[指定 NDIS 版本信息](specifying-ndis-version-information.md)

 

 






