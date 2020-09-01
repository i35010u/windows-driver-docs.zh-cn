---
title: 升级网络组件
description: 升级网络组件
ms.assetid: c183cd0a-53a7-4172-9cf8-70a93877c8a8
keywords:
- 通知对象 WDK 网络，升级网络组件
- 网络通知对象 WDK，升级网络组件
- 网络组件升级 WDK，通知对象
- 升级网络组件 WDK，通知对象
- 通知 WDK 网络，升级网络组件
- 升级网络组件 WDK，步骤
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01dbca9c4a024af952c29bb6bb9611ca79693a10
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215781"
---
# <a name="upgrading-network-components"></a>升级网络组件





网络组件由网络配置子系统升级。

**升级网络组件**

1.  网络配置子系统创建 notify 对象的一个实例，并调用该对象的 [**INetCfgComponentControl：： Initialize**](/previous-versions/windows/hardware/network/ff547729(v=vs.85)) 方法。 此方法初始化对象，并提供对组件和网络配置的所有方面的访问。

2.  当操作系统安装或升级到其他版本时，网络配置子系统将调用 notify 对象的 [**INetCfgComponentSetup：： Upgrade**](/previous-versions/windows/hardware/network/ff547783(v=vs.85)) 方法。

3.  子系统调用 notify 对象的 [**INetCfgComponentControl：： ApplyRegistryChanges**](/previous-versions/windows/hardware/network/ff547727(v=vs.85)) 方法来修改有关注册表中的网络组件的信息，然后调用 notify 对象的 [**INetCfgComponentControl：： ApplyPnpChanges**](/previous-versions/windows/hardware/network/ff547726(v=vs.85)) 方法，并传递 [**INetCfgPnpReconfigCallback**](/previous-versions/windows/hardware/network/ff547935(v=vs.85)) 接口以配置该组件的驱动程序和已升级的信息。

 

