---
title: 扩展专有 802.1X 安全方法的 UI
description: 扩展专有 802.1X 安全方法的 UI
keywords:
- 专有 802.1 X security WDK IHV UI Extension DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d9ca785ca1fa35d8b30b57f630c65efb66cf4c0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788395"
---
# <a name="extending-the-ui-for-proprietary-8021x-security-methods"></a>扩展专有 802.1X 安全方法的 UI




 

如果本机 802.11 IHV 扩展 DLL 支持专用的基于 X 的802.1 安全扩展插件，则本机 802.11 IHV UI 扩展 DLL 可以扩展网络配置用户界面的 (UI 的) **安全** "选项卡，以允许用户配置这些扩展。 有关扩展本机 802.11 802.1 X 模块的详细信息，请参阅 [本机 802.11 802.1 x 模块的接口](interface-to-the-native-802-11-802-1x-module.md)。

有关网络配置 UI 和其他本机802.11 组件的详细信息，请参阅 [本机802.11 软件体系结构](/previous-versions/windows/hardware/wireless/native-802-11-software-architecture)。

在显示 " **安全** " 选项卡之前，操作系统执行以下操作：

1.  通过对 [**IDot11ExtUI：： GetDot11ExtUIProperties**](/previous-versions/windows/hardware/wireless/ff553776(v=vs.85)) 方法的调用，在本机 802.11 IHV UI 扩展 DLL 中查询其安全属性扩展。 操作系统将值 **DOT11 \_ EXT \_ UI \_ KEYEXTENSION** 传递给方法的 *ExtType* 参数。

    **DOT11 \_ EXT \_ UI \_ KEYEXTENSION** 类型的属性扩展不提供与标准 Microsoft 安全设置互斥的安全设置。 相反，此类型的安全属性扩展提供了由 IHV 定义的 802.1 X 设置，可与 Microsoft 802.1 X 设置一起使用。

2.  通过调用扩展的 [**IDot11ExtUIProperty：： GetDot11ExtUIPropertyFriendlyName**](/previous-versions/windows/hardware/wireless/ff553768(v=vs.85)) 方法，查询 802.1 x 安全扩展插件的友好名称。

3.  查询扩展的 [**IDot11ExtUIProperty：:D ot11extuipropertyisstandardsecurity**](/previous-versions/windows/hardware/wireless/ff553760(v=vs.85)) 方法，以确定扩展是否支持安全类型扩展。 如果该方法将 *fIsStandardSecurity* 参数设置为 **FALSE**，则操作系统会将扩展的友好名称添加到 "**安全**" 选项卡上的 "**安全类型**" 列表中。

4.  当最终用户从 " **安全类型** " 列表中选择某一项时，操作系统将通过对每个扩展插件调用 [**IDot11ExtUIProperty：:D ot11extuipropertygetselected**](/previous-versions/windows/hardware/wireless/ff553753(v=vs.85)) 方法来做出响应，使其与最终用户的选择相匹配。 将方法的 *pfIsSelected* 参数的值返回为 **TRUE** 的第一个扩展将确定为所选扩展。 确认后，操作系统会突出显示最终用户所做的选择。

5.  调用所选属性扩展的 [**IDot11ExtUIProperty：:D ot11extuipropertyhasconfigurationui**](/previous-versions/windows/hardware/wireless/ff553756(v=vs.85)) 方法，以确定其是否具有可显示的自定义 UI 属性页。 如果该方法为该方法的 *fHasConfigurationUI* 参数返回的值为 **TRUE** ，则操作系统将显示 "**安全类型**" 列表旁边的 "**配置**" 按钮。

    如果最终用户单击 " **配置** " 按钮，操作系统将调用所选属性扩展的 [**IDot11ExtUIProperty：:D isplaydot11extuiproperty**](/previous-versions/windows/hardware/wireless/ff553749(v=vs.85)) 方法来显示扩展的自定义配置 UI。

6.  调用所选属性扩展的 [**IDot11ExtUIProperty：:D ot11extuipropertygetdisplayinfo**](/previous-versions/windows/hardware/wireless/ff553752(v=vs.85)) 方法。 通过此方法，本机 802.11 IHV UI 扩展 DLL 可将其他属性扩展返回到本机802.11 网络配置 UI 的 " **安全** " 选项卡。

    **IDot11ExtUIProperty：:D ot11extuipropertygetdisplayinfo** 方法返回所选属性扩展添加到 "**安全**" 选项卡的项列表。列表中的每个条目都设置为 [**DOT11 \_ EXT \_ UI \_ 属性 \_ 显示 \_ 信息**](/previous-versions/windows/hardware/drivers/ff548637(v=vs.85))结构。

    对于 Windows Vista，本机 802.11 IHV UI 扩展 DLL 只能将项添加到 "**安全**" 选项卡上的 "**加密**" 列表中。因此， [**DOT11 \_ ext \_ ui \_ 属性 \_ 显示 \_ 信息**](/previous-versions/windows/hardware/drivers/ff548637(v=vs.85))结构列表中的每一项都必须具有 **DOT11 \_ ext \_ ui \_ 显示 \_ 信息 \_ 类型** **DOT11 \_ ext \_ ui \_ 显示信息 \_ \_ 密码** 才能包含在 **加密** 列表中。

7.  当最终用户从 **加密** 列表中进行选择时，操作系统将调用所选属性扩展的 [**IDot11ExtUIProperty：:D ot11extuipropertysetdisplayinfo**](/previous-versions/windows/hardware/wireless/ff553763(v=vs.85)) 方法来处理与最终用户的选择相关联的配置文件数据。

 

 
