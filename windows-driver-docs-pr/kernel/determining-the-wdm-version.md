---
title: 确定 WDM 版本
description: 确定 WDM 版本
ms.assetid: 7ed288d9-6447-4b08-baf2-e7b743654ebd
keywords:
- WDM 驱动程序 WDK 内核，版本
- 版本 WDK WDM
- 兼容性 WDK WDM
- 跨系统兼容性 WDK WDM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0d01c7b6e4157dff8edc5685dbab8ba98d51625
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189075"
---
# <a name="determining-the-wdm-version"></a>确定 WDM 版本





跨系统 WDM 驱动程序应使用 [**IoIsWdmVersionAvailable**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioiswdmversionavailable) 例程来确定运行该程序的系统支持的 wdm 版本。 **IoIsWdmVersionAvailable**的参考页提供了一个 WDM 版本号列表。

有关驱动程序应处理的 WDM 之间的差异的信息，请参阅 [WDM 版本中的差异](differences-in-wdm-versions.md)。

 

