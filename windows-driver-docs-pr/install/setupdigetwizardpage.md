---
title: SetupDiGetWizardPage
description: SetupDiGetWizardPage
keywords:
- SetupDiGetWizardPage 设备和驱动程序安装
topic_type:
- apiref
api_name:
- SetupDiGetWizardPage
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5765a3b85c6ac7bb6f266677b8983d326af88f5e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838889"
---
# <a name="setupdigetwizardpage"></a>SetupDiGetWizardPage


**SetupDiGetWizardPage** 函数保留供系统使用。 有关向导页的信息，请参阅 DIF_NEWDEVICEWIZARD_ *XXX* 请求，例如 [**DIF_NEWDEVICEWIZARD_FINISHINSTALL**](dif-newdevicewizard-finishinstall.md)。

```cpp
HPROPSHEETPAGE
 SetupDiGetWizardPage(
 IN HDEVINFO DeviceInfoSet, 
 IN PSP_DEVINFO_DATA DeviceInfoData..OPTIONAL,
 IN PSP_INSTALLWIZARD_DATA InstallWizardData,
 IN DWORD PageType,
    IN DWORD Flags
 );
```

 

 





