---
title: 扩展专有 802.1X 安全方法的 UI
description: 扩展专有 802.1X 安全方法的 UI
ms.assetid: 3307179f-f30b-4234-a64d-4e771ac8673e
keywords:
- 专有 802.1x 安全 WDK IHV UI 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0bffd10830fa26ec8e4cd31437a3d3b91143f48
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386241"
---
# <a name="extending-the-ui-for-proprietary-8021x-security-methods"></a>扩展专有 802.1X 安全方法的 UI




 

如果本机 802.11 IHV 扩展 DLL 支持专有 802.1 X 基于安全扩展插件本机 802.11 IHV UI 扩展 DLL 可以扩展网络配置用户界面的 (UI)**安全**选项卡，以允许用户配置这些扩展。 有关扩展本机 802.11 802.1x 模块的详细信息，请参阅[接口的本机 802.11 802.1 X 模块](interface-to-the-native-802-11-802-1x-module.md)。

有关网络配置 UI 和其他本机 802.11 组件的详细信息，请参阅[本机 802.11 软件体系结构](native-802-11-software-architecture.md)。

它显示之前**安全**选项卡上，操作系统执行以下操作：

1.  查询通过调用其安全属性扩展的本机 802.11 IHV UI 扩展 DLL [ **IDot11ExtUI::GetDot11ExtUIProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff553776)方法。 操作系统将传递的值**DOT11\_EXT\_UI\_KEYEXTENSION**给方法的*ExtType*参数。

    类型的属性扩展**DOT11\_EXT\_UI\_KEYEXTENSION**不提供是互斥的标准的 Microsoft 安全设置的安全设置。 相反，这种类型的安全属性扩展中提供了 IHV 定义 802.1 X 与 Microsoft 802.1 X 设置一起使用的设置。

2.  通过调用扩展的查询的友好名称的安全扩展插件 802.1x [ **IDot11ExtUIProperty::GetDot11ExtUIPropertyFriendlyName** ](https://msdn.microsoft.com/library/windows/hardware/ff553768)方法。

3.  查询的扩展[ **IDot11ExtUIProperty::Dot11ExtUIPropertyIsStandardSecurity** ](https://msdn.microsoft.com/library/windows/hardware/ff553760)方法来确定扩展是否支持安全类型扩展。 如果该方法将设置*fIsStandardSecurity*参数**FALSE**，操作系统将添加到扩展的友好名称**安全类型**上列表**安全**选项卡。

4.  当最终用户选择中的项**安全类型**列表中，通过调用来响应操作系统[ **IDot11ExtUIProperty::Dot11ExtUIPropertyGetSelected** ](https://msdn.microsoft.com/library/windows/hardware/ff553753)每个扩展，以匹配的最终用户选择的方法。 返回的值的第一个扩展 **，则返回 TRUE**方法的*pfIsSelected*参数被确定为所选的扩展。 对此进行确认后，操作系统会突出显示的最终用户所做的选择。

5.  调用所选的属性扩展插件[ **IDot11ExtUIProperty::Dot11ExtUIPropertyHasConfigurationUI** ](https://msdn.microsoft.com/library/windows/hardware/ff553756)方法，以确定是否有可以显示的自定义 UI 属性页面。 如果该方法返回的值 **，则返回 TRUE**方法的*fHasConfigurationUI*参数，操作系统将显示**配置**旁边的按钮**安全类型**列表。

    如果最终用户单击**配置**按钮，操作系统将调用所选的属性扩展[ **IDot11ExtUIProperty::DisplayDot11ExtUIProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff553749)方法来显示该扩展的自定义配置 UI。

6.  调用所选的属性扩展插件[ **IDot11ExtUIProperty::Dot11ExtUIPropertyGetDisplayInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff553752)方法。 本机 802.11 IHV UI 扩展 DLL 可通过此方法返回对其他属性扩展**安全**本机 802.11 网络配置 UI 的选项卡。

    **IDot11ExtUIProperty::Dot11ExtUIPropertyGetDisplayInfo**方法返回的项的选定的属性扩展添加到列表**安全**选项卡。在列表中的每个条目的格式设置为[ **DOT11\_EXT\_UI\_属性\_显示\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff548637)结构。

    适用于 Windows Vista 本机 802.11 IHV UI 扩展 DLL 可以仅将项添加到**加密**上列出**安全**选项卡。因此，每个项目中的列表[ **DOT11\_EXT\_UI\_属性\_显示\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff548637)结构必须具有**DOT11\_EXT\_UI\_显示\_信息\_类型**的**DOT11\_EXT\_UI\_显示\_INFO\_密码**以包含在**加密**列表。

7.  当最终用户选择从**加密**列表中，操作系统将调用所选的属性扩展[ **IDot11ExtUIProperty::Dot11ExtUIPropertySetDisplayInfo**](https://msdn.microsoft.com/library/windows/hardware/ff553763)方法来处理与最终用户的所选内容关联的配置文件数据。

 

 





