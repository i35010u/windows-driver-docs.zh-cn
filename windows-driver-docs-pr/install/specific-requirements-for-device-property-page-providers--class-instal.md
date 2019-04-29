---
title: 设备属性页提供程序 （共同安装程序） 的要求
description: 设备属性页提供程序（辅助安装程序）的特定要求
ms.assetid: b57beaed-5e5f-499e-b973-532f33b7fb99
keywords:
- 设备属性页 WDK 设备安装，DIF_ADDPROPERTYPAGE_ADVANCED
- 属性页 WDK 设备安装，DIF_ADDPROPERTYPAGE_ADVANCED
- 自定义属性页 WDK 设备安装，DIF_ADDPROPERTYPAGE_ADVANCED
- DIF_ADDPROPERTYPAGE_ADVANCED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de9a6772f71692a9c07f00bc20f66f74c804410f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369429"
---
# <a name="specific-requirements-for-device-property-page-providers-co-installers"></a>设备属性页提供程序（辅助安装程序）的特定要求





一个[共同安装程序](writing-a-co-installer.md)，提供了一个或多个自定义设备属性页必须处理[ **DIF_ADDPROPERTYPAGE_ADVANCED** ](https://msdn.microsoft.com/library/windows/hardware/ff543656)设备安装函数 (DIF) 代码。 当用户单击时，设备管理器将发出此请求**属性**设备在设备管理器或控制面板中的选项卡。

以响应此请求，安装程序提供了有关每个自定义属性页的信息、 创建页，并将已创建的页添加到设备的动态属性页的列表。 安装程序初始化并返回请求的类安装参数的 SP_ADDPROPERTYPAGE_DATA 结构通过执行此操作。

如果用户更改任何属性，设备管理器发送[ **DIF_PROPERTYCHANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff543712) DIF 代码向安装程序安装程序通过调用来设置新的参数后[ **SetupDiSetDeviceInstallParams**](https://msdn.microsoft.com/library/windows/hardware/ff552141)。

有关如何创建自定义设备属性页的详细信息[共同安装程序](writing-a-co-installer.md)，请参阅[设备属性页提供程序的常规要求](general-requirements-for-device-property-page-providers.md)。

 

 





