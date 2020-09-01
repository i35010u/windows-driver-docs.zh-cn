---
title: 设置上下文以显示属性
description: 设置上下文以显示属性
ms.assetid: 9a5835b2-19a2-47fb-aa5b-87c3a9b955de
keywords:
- 通知对象 WDK 网络，上下文
- 网络通知对象 WDK，上下文
- 上下文 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b634011387949c3409dcb33473c0fb4848e4df5f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216930"
---
# <a name="setting-context-to-display-properties"></a>设置上下文以显示属性





Notify 对象可以设置上下文，以便在其中显示拥有对象的网络组件的属性。 Notify 对象在网络配置子系统调用对象的 [**INetCfgComponentPropertyUi：： SetContext**](/previous-versions/windows/hardware/network/ff547752(v=vs.85)) 方法之后但在子系统调用对象的 [**INetCfgComponentPropertyUi：： MergePropPages**](/previous-versions/windows/hardware/network/ff547746(v=vs.85)) 方法之前设置显示上下文。

当网络配置子系统调用 **SetContext**时，它会传递 **IUnknown** 接口。 **SetContext**对此**IUnknown**接口调用**QueryInterface**方法，以确定该子系统提供的特定对象的接口。

例如，网络配置子系统在调用**SetContext**时可以提供[**INetLanConnectionUiInfo**](/previous-versions/windows/hardware/network/ff548005(v=vs.85))接口。 **SetContext**可以使用**INetLanConnectionUiInfo**的[**GetDeviceGuid**](/previous-versions/windows/hardware/network/ff548012(v=vs.85))方法检索 LAN 设备的 GUID。 通知对象随后可以在此 LAN 设备的上下文中显示其网络组件的属性。 例如，TCP/IP 协议的 "通知" 对象可以显示与该适配器上下文中的特定 LAN 适配器相关联的 IP 地址。 这样做使用户能够为该适配器指定一个 IP 地址。

 

