---
title: 本机 802.11 IHV UI 扩展 COM 接口
description: 本机 802.11 IHV UI 扩展 COM 接口
keywords:
- IHV UI 扩展 DLL WDK 本机802.11，COM 接口
- COM 接口 WDK 本机 802.11 IHV UI 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a86bc93879e00888939d76e7fe37ea2cc0913b6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786107"
---
# <a name="native-80211-ihv-ui-extensions-com-interfaces"></a>本机 802.11 IHV UI 扩展 COM 接口




 

本机 802.11 IHV UI 扩展 DLL 实现了一个或多个下列 COM 接口：

<a href="" id="idot11extui"></a>**IDot11ExtUI**  
通过 **IDot11ExtUI** COM 接口，操作系统的本机802.11 网络配置 UI 可以与本机 802.11 IHV UI 扩展 DLL 交互。 例如，此 COM 接口提供了本机802.11 网络配置 UI 使用的方法来查询用于扩展操作系统802.11 连接和安全属性的 **IDot11ExtUIProperty** COM 接口的 DLL。

本机 802.11 IHV UI 扩展 DLL 必须提供 **IDot11ExtUI** COM 接口的实现。

有关此 COM 接口的详细信息，请参阅 [IDOT11EXTUI COM interface](/previous-versions/windows/hardware/wireless/ff553769(v=vs.85))。

<a href="" id="idot11extuiproperty"></a>**IDot11ExtUIProperty**  
通过 **IDot11ExtUIProperty** COM 接口，NATIVE 802.11 IHV UI 扩展 DLL 可以扩展本机802.11 网络配置 ui 显示的连接和安全属性。

**IDot11ExtUIProperty** COM 接口是可选的，仅当本机 802.11 IHV UI 扩展 DLL 支持操作系统的802.11 连接和安全属性的扩展时才是必需的。

本机 802.11 IHV UI 扩展 DLL 可提供 **IDot11ExtUIProperty** COM 接口的一个或多个实现，每个实现表示一个对本机802.11 属性的 IHV 定义的扩展。 DLL 可为安全设置提供一个或多个属性扩展。 对于 Windows Vista，DLL 不能为连接设置添加多个属性扩展。

有关此 COM 接口的详细信息，请参阅 [IDOT11EXTUIPROPERTY COM interface](/previous-versions/windows/hardware/wireless/ff553746(v=vs.85))。

<a href="" id="iwizardextension"></a>**IWizardExtension**  
本机 802.11 IHV UI 扩展 DLL 可提供 **IWizardExtension** COM 接口的一个或多个实现。 每个实现都支持显示一个或多个自定义 UI 页。 这些 UI 页面通过以下其中一项显示：

-   由本机 802.11 IHV 扩展 DLL 发出的外部请求。 有关此过程的详细信息，请参阅 [请求显示自定义 UI](requesting-the-display-of-a-custom-ui.md)。

-   操作系统执行的查询，用于确定本机 802.11 IHV 扩展 DLL 是否有要显示的自定义 UI。 有关此过程的详细信息，请参阅 [查询是否显示自定义 UI](querying-for-the-display-of-a-custom-ui.md)。

-   由本机 802.11 IHV UI 扩展 DLL 的组件发出的内部请求。

有关 **IWizardExtension** com 接口的详细信息，请参阅 [IWizardExtension com interface](/windows/win32/api/shobjidl/nn-shobjidl-iwizardextension)。

有关本机802.11 网络配置 UI 组件的详细信息，请参阅 [本机802.11 软件体系结构](/previous-versions/windows/hardware/wireless/native-802-11-software-architecture)。

 

 
