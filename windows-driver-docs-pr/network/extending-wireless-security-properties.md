---
title: 扩展无线安全属性
description: 扩展无线安全属性
ms.assetid: be6af188-fa60-4ac8-a699-97a3baaec6be
keywords:
- IHV UI 扩展 DLL WDK 本机802.11，安全属性
- 安全属性 WDK 本机 802.11 IHV UI 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73cfa53c5da4298c85b1ab8b272f6ba4e9718132
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215869"
---
# <a name="extending-wireless-security-properties"></a>扩展无线安全属性




 

本主题介绍本机 802.11 IHV UI 扩展 DLL 如何扩展通过网络配置用户界面 (UI) 显示的 " **安全** " 选项卡的属性。 在这种情况下，本机 802.11 IHV UI 扩展 DLL 会将属性添加到专用安全设置的 " **安全** " 选项卡，这些设置与本机 802.11 802.1 x 模块相互排斥。

本机 802.11 IHV UI 扩展 DLL 还可以扩展本机 802.11 802.1 X 模块支持的安全和加密方法。 有关 DLL 如何实现此操作的详细信息，请参阅 [扩展 Microsoft 802.1 x 安全设置](extending-microsoft-802-1x-security-settings.md)。

有关网络配置 UI 和其他本机802.11 组件的详细信息，请参阅 [本机802.11 软件体系结构](/previous-versions/windows/hardware/wireless/native-802-11-software-architecture)。

在显示 " **安全** " 选项卡之前，操作系统执行以下操作：

1.  通过对 [**IDot11ExtUI：： GetDot11ExtUIProperties**](/previous-versions/windows/hardware/wireless/ff553776(v=vs.85)) 方法的调用，在本机 802.11 IHV UI 扩展 DLL 中查询其安全属性扩展。 操作系统将 **DOT11 \_ EXT \_ UI \_ SECURITY** 的值传递给该方法的 *ExtType* 参数。

    如果本机 802.11 IHV UI 扩展 DLL 支持类型为 **DOT11 \_ EXT \_ ui \_ SECURITY**的一个或多个属性，则 Dll 将通过方法的 *PPDOT11EXTUIPROPERTY* 参数返回 (，) Dll 支持的安全属性扩展的 [IDot11ExtUIProperty COM 接口](/previous-versions/windows/hardware/wireless/ff553746(v=vs.85)) 的列表。 有关用于扩展安全属性的 COM 接口的详细信息，请参阅 [本机 802.11 IHV UI 扩展 Com 接口](native-802-11-ihv-ui-extensions-com-interfaces.md)。

2.  通过调用扩展的 [**IDot11ExtUIProperty：： GetDot11ExtUIPropertyFriendlyName**](/previous-versions/windows/hardware/wireless/ff553768(v=vs.85)) 方法查询安全扩展插件的友好名称。 操作系统将友好名称添加到 " **安全** " 选项卡底部的 "专有安全设置" 列表中。

3.  如果最终用户从该列表中选择一项，则操作系统将调用每个安全扩展程序的[IDOT11EXTUIPROPERTY COM 接口](/previous-versions/windows/hardware/wireless/ff553746(v=vs.85))的[**IDot11ExtUIProperty：:D ot11extuipropertygetselected**](/previous-versions/windows/hardware/wireless/ff553753(v=vs.85))方法。 如果第一个扩展的值为 TRUE，则该方法的*pfIsSelected*参数的值为**TRUE** 。 然后，将突出显示列表中选定的项。

4.  查询选定设置的 [**IDot11ExtUIProperty：:D ot11extuipropertyhasconfigurationui**](/previous-versions/windows/hardware/wireless/ff553756(v=vs.85)) 方法，以确定其是否具有可显示的自定义 UI 属性页。 如果该方法返回时，将 *fHasConfigurationUI* 参数设置为 **TRUE**，则操作系统会将 " **配置** " 按钮添加到专用安全设置列表的旁边。

如果所选专用安全设置支持配置用户界面，最终用户单击 " **配置** " 按钮，操作系统将调用设置的 [**IDot11ExtUIProperty：:D isplaydot11extuiproperty**](/previous-versions/windows/hardware/wireless/ff553749(v=vs.85)) 方法来启动自定义 UI。 操作系统通过方法的 *bstrIHVProfile* 参数传递设置的当前配置文件数据。

配置文件数据的格式为由 &lt; IHV &gt; &lt; /IHV &gt; XML 标记界定的 xml 片段。 这些标记中的 XML 数据特定于 IHV 的实现，对操作系统不透明。 有关本机802.11 配置文件数据格式的详细信息，请参阅 Microsoft Windows SDK 中的文档。

如果通过自定义 UI 更改配置文件数据，设置的 [**IDot11ExtUIProperty：:D isplaydot11extuiproperty**](/previous-versions/windows/hardware/wireless/ff553749(v=vs.85)) 方法必须在返回前执行以下操作：

-   为修改后的配置文件数据分配字符串缓冲区，并通过方法的 *bstrModifiedIHVProfile* 参数返回指向缓冲区的指针。
    **注意**   设置的[**IDot11ExtUIProperty：:D isplaydot11extuiproperty**](/previous-versions/windows/hardware/wireless/ff553749(v=vs.85))方法不能修改*bstrIHVProfile*参数所引用的数据。

     

-   将 *pbIsModified* 参数设置为 **TRUE**。

 

 