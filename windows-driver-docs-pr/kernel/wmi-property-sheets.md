---
title: WMI 属性表
description: WMI 属性表
keywords:
- WMI WDK 内核，属性表
- 属性表 WDK WMI
- 设备属性表 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3153965091b31911da9106e2db6a4e03db999c00
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782653"
---
# <a name="wmi-property-sheets"></a>WMI 属性表





用户友好的驱动程序允许用户通过其 **设备管理器** 属性表来控制其设置。 有关设备管理器的说明，请参阅 [使用设备管理器](../install/using-device-manager.md) 。

驱动程序可以使用 [wmi 通用属性页提供程序](wmi-generic-property-page-provider.md)在其属性表上自动公开其实现的所有 WMI 类。

驱动程序可以通过支持特定的 WMI 类 Guid 来启用 **设备管理器** 属性表的 "**电源管理**" 选项卡上的某些控件。 有关详细信息，请参阅 [WMI 和电源管理选项卡](wmi-and-the-power-management-tab.md) 。

 

