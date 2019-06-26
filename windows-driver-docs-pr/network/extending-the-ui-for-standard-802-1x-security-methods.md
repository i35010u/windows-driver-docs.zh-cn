---
title: 扩展标准 802.1X 安全方法的 UI
description: 扩展标准 802.1X 安全方法的 UI
ms.assetid: e80e82e9-3ad3-48d0-a569-169de356ebba
keywords:
- 标准 802.1x 安全 WDK IHV UI 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e6aec8f9d284b254e96b9d146f49eca268ac4d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363425"
---
# <a name="extending-the-ui-for-standard-8021x-security-methods"></a>扩展标准 802.1X 安全方法的 UI




 

本机 802.11 IHV UI 扩展 DLL 如果本机 802.11 IHV 扩展 DLL 支持可与操作系统的 802.1x 安全方法的专有加密扩展插件，可以扩展在网络配置用户界面 (UI) s **安全**选项卡，以允许用户配置这些扩展。 有关扩展本机 802.11 802.1x 模块的详细信息，请参阅[接口的本机 802.11 802.1 X 模块](interface-to-the-native-802-11-802-1x-module.md)。

有关网络配置 UI 和其他本机 802.11 组件的详细信息，请参阅[本机 802.11 软件体系结构](native-802-11-software-architecture.md)。

它显示之前**安全**选项卡上，操作系统执行以下操作：

1.  查询通过调用其安全属性扩展的本机 802.11 IHV UI 扩展 DLL [ **IDot11ExtUI::GetDot11ExtUIProperties** ](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff553776(v=vs.85))方法。 操作系统将传递的值**DOT11\_EXT\_UI\_KEYEXTENSION**给方法的*ExtType*参数。

    类型的属性扩展**DOT11\_EXT\_UI\_KEYEXTENSION**不提供是互斥的标准的 Microsoft 安全设置的安全设置。 相反，这种类型的安全属性扩展中提供了 IHV 定义 802.1 X 与 Microsoft 802.1 X 设置一起使用的设置。

2.  通过调用扩展的查询的友好名称的安全扩展插件 802.1x [ **IDot11ExtUIProperty::GetDot11ExtUIPropertyFriendlyName** ](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff553768(v=vs.85))方法。

3.  查询的扩展[ **IDot11ExtUIProperty::Dot11ExtUIPropertyIsStandardSecurity** ](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff553760(v=vs.85))方法来确定扩展是否支持安全类型扩展。 如果该方法将设置*fIsStandardSecurity*参数**TRUE**，操作系统将不会添加到扩展的友好名称**安全类型**上列表**安全**选项卡。

    在此情况下，该扩展将功能添加到支持的操作系统的安全设置。 该方法指定安全设置，它通过扩展的类型*dot11ExtUISecurityType*参数。

4.  当最终用户选择中的项**安全类型**列表中，通过调用来响应操作系统[ **IDot11ExtUIProperty::Dot11ExtUIPropertyGetSelected** ](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff553753(v=vs.85))每个扩展，以匹配的最终用户选择的方法。 返回的值的第一个扩展 **，则返回 TRUE**方法的*pfIsSelected*参数被确定为所选的扩展。 对此进行确认后，操作系统会突出显示的最终用户所做的选择。

5.  当最终用户选择一个标准的安全设置的项**安全类型**列表中，操作系统调用[ **IDot11ExtUIProperty::Dot11ExtUIPropertyGetDisplayInfo**](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff553752(v=vs.85))扩展安全方法的属性扩展的方法。 通过**IDot11ExtUIProperty::Dot11ExtUIPropertyGetDisplayInfo**方法，本机 802.11 IHV UI 扩展 DLL 可返回要添加到其他项**安全**本机 802.11 的选项卡网络配置 UI。

    **IDot11ExtUIProperty::Dot11ExtUIPropertyGetDisplayInfo**方法返回的属性扩展插件支持扩展的显示属性列表。 列表中的每个项的格式设置为[ **DOT11\_EXT\_UI\_属性\_显示\_信息**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548637(v=vs.85))结构。

    适用于 Windows Vista 本机 802.11 IHV UI 扩展 DLL 可以仅将项添加到**加密**上列出**安全**选项卡。因此，列表中每个条目[ **DOT11\_EXT\_UI\_属性\_显示\_信息**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548637(v=vs.85))结构必须具有**DOT11\_EXT\_UI\_显示\_信息\_类型**的**DOT11\_EXT\_UI\_显示\_INFO\_密码**以包含在**加密**列表。

6.  当最终用户选择从**加密**列表中，操作系统将调用的属性扩展[ **IDot11ExtUIProperty::Dot11ExtUIPropertySetDisplayInfo** ](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff553763(v=vs.85))方法来处理与最终用户的所选内容关联的配置文件数据。

 

 





