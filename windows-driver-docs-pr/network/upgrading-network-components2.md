---
title: 升级网络组件
description: 升级网络组件
ms.assetid: c183cd0a-53a7-4172-9cf8-70a93877c8a8
keywords:
- 通知对象 WDK 网络、 升级网络组件
- 网络通知对象 WDK、 升级网络组件
- 网络组件升级，WDK，通知对象
- 升级网络组件 WDK，通知对象
- 通知 WDK 网络、 升级网络组件
- 升级网络组件 WDK，步骤
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 749a9c147b48a9200f53526a1709b2cd5904ea05
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369010"
---
# <a name="upgrading-network-components"></a>升级网络组件





通过网络配置子系统会升级网络组件。

**若要升级网络组件**

1.  网络配置子系统创建通知对象的实例并调用该对象的[ **INetCfgComponentControl::Initialize** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547729(v=vs.85))方法。 此方法将对象初始化，并提供对组件和网络配置的所有方面的访问。

2.  当操作系统安装或升级到不同的版本时，网络配置子系统调用通知对象[ **INetCfgComponentSetup::Upgrade** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547783(v=vs.85))方法。

3.  子系统调用通知对象的[ **INetCfgComponentControl::ApplyRegistryChanges** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547727(v=vs.85))方法来修改注册表中的网络组件有关的信息，然后调用通知对象的[ **INetCfgComponentControl::ApplyPnpChanges** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547726(v=vs.85))方法，并传递[ **INetCfgPnpReconfigCallback** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547935(v=vs.85))若要配置该组件的驱动程序与已升级的信息的接口。

 

 





