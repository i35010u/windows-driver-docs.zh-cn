---
title: 确定 WDM 版本
description: 确定 WDM 版本
keywords:
- WDM 驱动程序 WDK 内核，版本
- 版本 WDK WDM
- 兼容性 WDK WDM
- 跨系统兼容性 WDK WDM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97459e75c6ad45629ca4a7787ebe47c96d0f1a66
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813059"
---
# <a name="determining-the-wdm-version"></a>确定 WDM 版本





跨系统 WDM 驱动程序应使用 [**IoIsWdmVersionAvailable**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioiswdmversionavailable) 例程来确定运行该程序的系统支持的 wdm 版本。 **IoIsWdmVersionAvailable** 的参考页提供了一个 WDM 版本号列表。

有关驱动程序应处理的 WDM 之间的差异的信息，请参阅 [WDM 版本中的差异](differences-in-wdm-versions.md)。

 

