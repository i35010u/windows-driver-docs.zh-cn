---
title: 设置上下文以显示属性
description: 设置上下文以显示属性
ms.assetid: 9a5835b2-19a2-47fb-aa5b-87c3a9b955de
keywords:
- 通知对象 WDK 网络、 上下文
- 网络通知 WDK，对象上下文
- 上下文 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cd7231e7b457b1a03ed514e31ca20415d4d645e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562519"
---
# <a name="setting-context-to-display-properties"></a>设置上下文以显示属性





通知对象可以设置在其中以显示该对象所属的网络组件的属性的上下文。 通知对象集之后的网络配置子系统调用该对象的显示上下文[ **INetCfgComponentPropertyUi::SetContext** ](https://msdn.microsoft.com/library/windows/hardware/ff547752)但子系统之前调用的方法对象的[ **INetCfgComponentPropertyUi::MergePropPages** ](https://msdn.microsoft.com/library/windows/hardware/ff547746)方法。

当调用网络配置子系统**SetContext**，它将传递**IUnknown**接口。 **SetContext**调用**QueryInterface**方法对此**IUnknown**接口，以确定子系统提供的特定对象的接口。

例如，可以提供网络配置子系统[ **INetLanConnectionUiInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff548005)接口调用时**SetContext**。 **SetContext**可以使用[ **GetDeviceGuid** ](https://msdn.microsoft.com/library/windows/hardware/ff548012)方法**INetLanConnectionUiInfo**检索 LAN 设备的 GUID。 通知对象随后可以在此 LAN 设备的上下文中显示其网络组件的属性。 例如，TCP/IP 协议的通知对象可以显示与该适配器的上下文中的特定 LAN 适配器相关联的 IP 地址。 这样做可以让用户指定为该适配器的 IP 地址。

 

 





