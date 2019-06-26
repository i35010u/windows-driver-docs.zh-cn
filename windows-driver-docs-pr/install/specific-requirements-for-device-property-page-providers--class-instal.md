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
ms.openlocfilehash: 969c786ab427c18ba75381f0fc56e2b6014211d0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385891"
---
# <a name="specific-requirements-for-device-property-page-providers-co-installers"></a>设备属性页提供程序（辅助安装程序）的特定要求





一个[共同安装程序](writing-a-co-installer.md)，提供了一个或多个自定义设备属性页必须处理[ **DIF_ADDPROPERTYPAGE_ADVANCED** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-addpropertypage-advanced)设备安装函数 (DIF) 代码。 当用户单击时，设备管理器将发出此请求**属性**设备在设备管理器或控制面板中的选项卡。

以响应此请求，安装程序提供了有关每个自定义属性页的信息、 创建页，并将已创建的页添加到设备的动态属性页的列表。 安装程序初始化并返回请求的类安装参数的 SP_ADDPROPERTYPAGE_DATA 结构通过执行此操作。

如果用户更改任何属性，设备管理器发送[ **DIF_PROPERTYCHANGE** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-propertychange) DIF 代码向安装程序安装程序通过调用来设置新的参数后[ **SetupDiSetDeviceInstallParams**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinstallparamsa)。

有关如何创建自定义设备属性页的详细信息[共同安装程序](writing-a-co-installer.md)，请参阅[设备属性页提供程序的常规要求](general-requirements-for-device-property-page-providers.md)。

 

 





