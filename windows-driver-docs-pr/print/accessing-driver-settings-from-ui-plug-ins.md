---
title: 从 UI 插件访问驱动程序设置
description: 从 UI 插件访问驱动程序设置
keywords:
- 用户界面插件 WDK 打印，访问驱动程序设置
- UI 插件 WDK 打印，访问驱动程序设置
- 状态信息 WDK 打印插件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44fee1e2d201bcca5e15257e5b3aa1417bffab27
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812437"
---
# <a name="accessing-driver-settings-from-ui-plug-ins"></a>从 UI 插件访问驱动程序设置





UI 插件可以获取打印机功能和其他内部信息的当前状态。 [**IPrintOemDriverUI：:D rvgetdriversetting**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverui-drvgetdriversetting) COM 接口方法是在 Microsoft 的打印机驱动程序的打印机接口 DLL 内实现的，并且可以由 UI 插件调用。

此外，以下方法允许 UI 插件修改驱动程序信息：

[**IPrintOemDriverUI：:D rvupdateuisetting**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverui-drvupdateuisetting) 允许 UI 插件在用户修改了驱动程序设置时通知驱动程序。

[**IPrintOemDriverUI：:D rvupgraderegistrysetting**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverui-drvupgraderegistrysetting) 允许 UI 插件修改注册表中的设备设置，以便可以更新旧驱动程序版本使用的注册表设置。

 

