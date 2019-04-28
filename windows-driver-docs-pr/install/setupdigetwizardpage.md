---
title: SetupDiGetWizardPage
description: SetupDiGetWizardPage
ms.assetid: c43ee948-10aa-4b8f-91d0-0f3baf8ccf16
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
ms.openlocfilehash: a4898a9e6ea9445f26954a166de9f077240a31d4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348630"
---
# <a name="setupdigetwizardpage"></a>SetupDiGetWizardPage


**SetupDiGetWizardPage**函数保留供系统使用。 有关向导页的信息，请参阅 DIF_NEWDEVICEWIZARD_*XXX*请求时，例如， [ **DIF_NEWDEVICEWIZARD_FINISHINSTALL**](dif-newdevicewizard-finishinstall.md)。

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

 

 





