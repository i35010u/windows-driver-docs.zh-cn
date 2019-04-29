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
ms.openlocfilehash: 96c4b89da09db5b095a48b3d664c80bc7caed257
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387145"
---
# <a name="upgrading-network-components"></a>升级网络组件





通过网络配置子系统会升级网络组件。

**若要升级网络组件**

1.  网络配置子系统创建通知对象的实例并调用该对象的[ **INetCfgComponentControl::Initialize** ](https://msdn.microsoft.com/library/windows/hardware/ff547729)方法。 此方法将对象初始化，并提供对组件和网络配置的所有方面的访问。

2.  当操作系统安装或升级到不同的版本时，网络配置子系统调用通知对象[ **INetCfgComponentSetup::Upgrade** ](https://msdn.microsoft.com/library/windows/hardware/ff547783)方法。

3.  子系统调用通知对象的[ **INetCfgComponentControl::ApplyRegistryChanges** ](https://msdn.microsoft.com/library/windows/hardware/ff547727)方法来修改注册表中的网络组件有关的信息，然后调用通知对象的[ **INetCfgComponentControl::ApplyPnpChanges** ](https://msdn.microsoft.com/library/windows/hardware/ff547726)方法，并传递[ **INetCfgPnpReconfigCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff547935)若要配置该组件的驱动程序与已升级的信息的接口。

 

 





