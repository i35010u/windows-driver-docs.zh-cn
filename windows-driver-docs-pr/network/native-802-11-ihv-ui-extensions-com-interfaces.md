---
title: 本机 802.11 IHV UI 扩展 COM 接口
description: 本机 802.11 IHV UI 扩展 COM 接口
ms.assetid: 95487686-17a0-43e2-93bb-99b3adb9dadd
keywords:
- IHV UI 扩展 DLL WDK 本机 802.11，COM 接口
- COM 接口 WDK 本机 802.11 IHV UI 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a44c0b76244ba7d05efbcbdcbe1912549096686b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383618"
---
# <a name="native-80211-ihv-ui-extensions-com-interfaces"></a>本机 802.11 IHV UI 扩展 COM 接口




 

本机 802.11 IHV UI 扩展 DLL 实现一个或多个以下的 COM 接口：

<a href="" id="idot11extui"></a>**IDot11ExtUI**  
通过**IDot11ExtUI** COM 接口，操作系统的本机 802.11 网络配置 UI 可与本机 802.11 IHV UI 扩展 DLL 交互。 例如，此 COM 接口提供本机 802.11 网络配置 UI 用于查询的 DLL 的方法**IDot11ExtUIProperty** COM 接口，用于扩展操作系统的 802.11 连接和安全属性。

本机 802.11 IHV UI 扩展 DLL 必须提供的实现**IDot11ExtUI** COM 接口。

有关此 COM 接口的详细信息，请参阅[IDot11ExtUI COM 接口](https://msdn.microsoft.com/library/windows/hardware/ff553769)。

<a href="" id="idot11extuiproperty"></a>**IDot11ExtUIProperty**  
通过**IDot11ExtUIProperty** COM 接口，本机 802.11 IHV UI 扩展 DLL 可以扩展本机 802.11 网络配置 UI 显示的连接和安全属性。

**IDot11ExtUIProperty** COM 接口是可选的仅需要本机 802.11 IHV UI 扩展 DLL 是否支持对操作系统的 802.11 连接和安全属性的扩展。

本机 802.11 IHV UI 扩展 DLL 可以提供的一个或多个实现**IDot11ExtUIProperty** COM 接口，与每个实现，后者表示 IHV 定义扩展到本机 802.11 属性。 该 DLL 可以提供一个或多个属性扩展的安全设置。 适用于 Windows Vista DLL 可以添加多个属性扩展中的连接设置。

有关此 COM 接口的详细信息，请参阅[IDot11ExtUIProperty COM 接口](https://msdn.microsoft.com/library/windows/hardware/ff553746)。

<a href="" id="iwizardextension"></a>**IWizardExtension**  
本机 802.11 IHV UI 扩展 DLL 可以提供的一个或多个实现**IWizardExtension** COM 接口。 每个实现都支持一个或多个自定义 UI 页的显示。 这些 UI 页将显示通过以下项之一：

-   本机 802.11 IHV 扩展 DLL 由外部请求。 有关此过程的详细信息，请参阅[请求的自定义用户界面显示](requesting-the-display-of-a-custom-ui.md)。

-   由操作系统确定本机 802.11 IHV 扩展 DLL 是否具有自定义 UI 以显示查询。 有关此过程的详细信息，请参阅[查询的自定义用户界面显示](querying-for-the-display-of-a-custom-ui.md)。

-   内部请求所做的本机 802.11 IHV UI 扩展 DLL 的一个组件。

有关详细信息**IWizardExtension** COM 接口，请参阅[IWizardExtension COM 接口](https://go.microsoft.com/fwlink/p/?linkid=56607)。

有关本机 802.11 网络配置 UI 组件的详细信息，请参阅[本机 802.11 软件体系结构](native-802-11-software-architecture.md)。

 

 





