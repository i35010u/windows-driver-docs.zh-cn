---
title: 扩展标准 802.1X 安全方法的 UI
description: 扩展标准 802.1X 安全方法的 UI
ms.assetid: e80e82e9-3ad3-48d0-a569-169de356ebba
keywords:
- 标准 802.1 X security WDK IHV UI Extension DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df0d45c1ba8948ca1274b5de026694cdaeeca4cb
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212185"
---
# <a name="extending-the-ui-for-standard-8021x-security-methods"></a>扩展标准 802.1X 安全方法的 UI




 

如果本机 802.11 IHV 扩展 DLL 支持可以与操作系统的 802.1 X 安全方法一起使用的专有加密扩展，则本机 802.11 IHV UI 扩展 DLL 可以扩展网络配置用户界面的 (UI ") s **安全** " 选项卡，以允许用户配置这些扩展。 有关扩展本机 802.11 802.1 X 模块的详细信息，请参阅 [本机 802.11 802.1 x 模块的接口](interface-to-the-native-802-11-802-1x-module.md)。

有关网络配置 UI 和其他本机802.11 组件的详细信息，请参阅 [本机802.11 软件体系结构](/previous-versions/windows/hardware/wireless/native-802-11-software-architecture)。

在显示 " **安全** " 选项卡之前，操作系统执行以下操作：

1.  通过对 [**IDot11ExtUI：： GetDot11ExtUIProperties**](/previous-versions/windows/hardware/wireless/ff553776(v=vs.85)) 方法的调用，在本机 802.11 IHV UI 扩展 DLL 中查询其安全属性扩展。 操作系统将值 **DOT11 \_ EXT \_ UI \_ KEYEXTENSION** 传递给方法的 *ExtType* 参数。

    **DOT11 \_ EXT \_ UI \_ KEYEXTENSION**类型的属性扩展不提供与标准 Microsoft 安全设置互斥的安全设置。 相反，此类型的安全属性扩展提供了由 IHV 定义的 802.1 X 设置，可与 Microsoft 802.1 X 设置一起使用。

2.  通过调用扩展的 [**IDot11ExtUIProperty：： GetDot11ExtUIPropertyFriendlyName**](/previous-versions/windows/hardware/wireless/ff553768(v=vs.85)) 方法，查询 802.1 x 安全扩展插件的友好名称。

3.  查询扩展的 [**IDot11ExtUIProperty：:D ot11extuipropertyisstandardsecurity**](/previous-versions/windows/hardware/wireless/ff553760(v=vs.85)) 方法，以确定扩展是否支持安全类型扩展。 如果该方法将*fIsStandardSecurity*参数设置为**TRUE**，则操作系统不会将该扩展的友好名称添加到 "**安全**" 选项卡上的 "**安全类型**" 列表中。

    在这种情况下，扩展会向操作系统支持的安全设置添加功能。 方法指定通过 *dot11ExtUISecurityType* 参数扩展的安全设置类型。

4.  当最终用户从 " **安全类型** " 列表中选择某一项时，操作系统将通过对每个扩展插件调用 [**IDot11ExtUIProperty：:D ot11extuipropertygetselected**](/previous-versions/windows/hardware/wireless/ff553753(v=vs.85)) 方法来做出响应，使其与最终用户的选择相匹配。 将方法的*pfIsSelected*参数的值返回为**TRUE**的第一个扩展将确定为所选扩展。 确认后，操作系统会突出显示最终用户所做的选择。

5.  当最终用户从 " **安全类型** " 列表中为标准安全设置选择项时，操作系统将调用扩展安全方法的属性扩展的 [**IDot11ExtUIProperty：:D ot11extuipropertygetdisplayinfo**](/previous-versions/windows/hardware/wireless/ff553752(v=vs.85)) 方法。 通过 **IDot11ExtUIProperty：:D ot11extuipropertygetdisplayinfo** 方法，本机 802.11 IHV UI 扩展 DLL 可以返回要添加到本机802.11 网络配置 UI 的 " **安全** " 选项卡的其他项。

    **IDot11ExtUIProperty：:D ot11extuipropertygetdisplayinfo**方法返回属性扩展所支持的扩展显示属性的列表。 列表中的每一项都设置为 [**DOT11 \_ EXT \_ UI \_ 属性 \_ 显示 \_ 信息**](/previous-versions/windows/hardware/drivers/ff548637(v=vs.85)) 结构。

    对于 Windows Vista，本机 802.11 IHV UI 扩展 DLL 只能将项添加到 "**安全**" 选项卡上的 "**加密**" 列表中。因此， [**DOT11 \_ ext \_ ui \_ 属性 \_ \_ **](/previous-versions/windows/hardware/drivers/ff548637(v=vs.85))的列表中的每个条目都必须具有**DOT11 \_ ext ui \_ \_ 显示 \_ 信息 \_ 类型** **DOT11 \_ ext \_ ui \_ 显示信息 \_ \_ 密码**才能包含在**加密**列表中。

6.  当最终用户从 **加密** 列表中进行选择时，操作系统将调用属性扩展的 [**IDot11ExtUIProperty：:D ot11extuipropertysetdisplayinfo**](/previous-versions/windows/hardware/wireless/ff553763(v=vs.85)) 方法来处理与最终用户的选择相关联的配置文件数据。

 

 