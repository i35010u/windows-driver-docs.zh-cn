---
title: 确定 WDM 版本
description: 确定 WDM 版本
ms.assetid: 7ed288d9-6447-4b08-baf2-e7b743654ebd
keywords:
- WDM 驱动程序 WDK 内核版本
- 版本 WDK WDM
- WDK WDM 的兼容性
- 跨系统的兼容性 WDK WDM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: de1d9dc98cb1f47e9101e91883ae98dd2639424e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371269"
---
# <a name="determining-the-wdm-version"></a>确定 WDM 版本





跨系统 WDM 驱动程序应使用[ **IoIsWdmVersionAvailable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioiswdmversionavailable)例程，以确定哪个版本的 WDM 支持通过在其运行的系统。 参考页**IoIsWdmVersionAvailable**提供了一系列 WDM 版本号。

WDM 驱动程序应处理的差异的信息，请参阅[WDM 版本差异](differences-in-wdm-versions.md)。

 

 




