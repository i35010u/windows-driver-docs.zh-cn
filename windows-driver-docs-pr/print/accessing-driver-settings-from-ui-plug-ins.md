---
title: 从 UI 插件访问驱动程序设置
description: 从 UI 插件访问驱动程序设置
ms.assetid: 898e1cfb-851b-403e-a88b-d38c505c1390
keywords:
- 用户界面插件 WDK 打印，访问驱动程序设置
- UI 插件 WDK 打印，访问驱动程序设置
- 状态信息 WDK 打印的插件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d996039f271d8acf312cc2532b3d0aa4f2bd8688
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385702"
---
# <a name="accessing-driver-settings-from-ui-plug-ins"></a>从 UI 插件访问驱动程序设置





UI 插件可以获取打印机功能和其他内部信息的当前状态。 [ **IPrintOemDriverUI::DrvGetDriverSetting** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriverui-drvgetdriversetting) COM 接口方法在 Microsoft 的打印机驱动程序的打印机接口 DLL 中实现且可通过 UI 插件调用。

此外，下面的方法允许 UI 插件来修改驱动程序信息：

[**IPrintOemDriverUI::DrvUpdateUISetting** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriverui-drvupdateuisetting)允许 UI 插件在用户已修改驱动程序设置时通知该驱动程序。

[**IPrintOemDriverUI::DrvUpgradeRegistrySetting** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriverui-drvupgraderegistrysetting)允许 UI 插件，以修改在注册表中，设备设置，以便可以更新旧驱动程序版本使用的注册表设置。

 

 




