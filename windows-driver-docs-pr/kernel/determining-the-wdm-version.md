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
ms.openlocfilehash: a9c0602d202f47da2018dc8220f391cc5dac4842
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828368"
---
# <a name="determining-the-wdm-version"></a>确定 WDM 版本





跨系统 WDM 驱动程序应使用[**IoIsWdmVersionAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioiswdmversionavailable)例程来确定运行该程序的系统支持的 wdm 版本。 **IoIsWdmVersionAvailable**的参考页提供了一个 WDM 版本号列表。

有关驱动程序应处理的 WDM 之间的差异的信息，请参阅[WDM 版本中的差异](differences-in-wdm-versions.md)。

 

 




