---
title: 扩展无线连接属性
description: 扩展无线连接属性
keywords:
- IHV UI 扩展 DLL WDK 本机802.11，无线连接属性
- 无线连接属性 WDK 本机 802.11 IHV UI 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cac6f66132f4630b8437f40a37cfc4d0fe43bb89
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788376"
---
# <a name="extending-wireless-connection-properties"></a>扩展无线连接属性




 

本主题介绍本机 802.11 IHV UI 扩展 DLL 如何扩展通过网络配置用户界面 (UI) 显示的 " **连接** " 选项卡的属性。 在这种情况下，本机 802.11 IHV UI 扩展 DLL 会将属性添加到专用连接设置的 " **连接** " 选项卡中。

有关网络配置 UI 和其他本机802.11 组件的详细信息，请参阅 [本机802.11 软件体系结构](/previous-versions/windows/hardware/wireless/native-802-11-software-architecture)。

在显示 " **连接** " 选项卡之前，操作系统执行以下操作：

1.  通过对 [**IDot11ExtUI：： GetDot11ExtUIProperties**](/previous-versions/windows/hardware/wireless/ff553776(v=vs.85)) 方法的调用，在本机 802.11 IHV UI 扩展 DLL 中查询其连接属性。 操作系统将 **DOT11 \_ EXT \_ UI \_ 连接** 值传递到该方法的 *ExtType* 参数。

    如果本机 802.11 IHV UI 扩展 DLL 支持类型为 **DOT11 \_ EXT \_ ui \_ 连接** 的属性，则 DLL 将通过方法的 *ppDot11ExtUIProperty* 参数) 返回 [ (，该参数将实现](/previous-versions/windows/hardware/wireless/ff553746(v=vs.85))连接属性扩展。 有关用于扩展连接属性的 COM 接口的详细信息，请参阅 [本机 802.11 IHV UI 扩展 Com 接口](native-802-11-ihv-ui-extensions-com-interfaces.md)。

    **注意**  对于 Windows Vista，本机 802.11 IHV UI 扩展 DLL 不得为连接属性扩展返回多个 [IDOT11EXTUI COM 接口](/previous-versions/windows/hardware/wireless/ff553769(v=vs.85)) 。

     

2.  如果本机 802.11 IHV UI 扩展 DLL 支持连接属性，则操作系统将通过调用扩展的 [**IDot11ExtUIProperty：： GetDot11ExtUIPropertyFriendlyName**](/previous-versions/windows/hardware/wireless/ff553768(v=vs.85)) 方法来查询属性扩展的友好名称。 操作系统在文本 "启用 *xxx* 连接设置" 中插入友好名称，其中 "*xxx*" 是属性扩展的友好名称。 操作系统在 " **连接** " 选项卡上显示此文本以及一个复选框。

3.  查询扩展，以确定它是否有可显示的自定义 UI 属性。 操作系统通过调用扩展的 [**IDot11ExtUIProperty：:D ot11extuipropertyhasconfigurationui**](/previous-versions/windows/hardware/wireless/ff553756(v=vs.85)) 方法来执行此操作。 如果连接属性扩展支持自定义 UI 属性，则操作系统会在该属性的复选框下方添加一个 " **配置** " 按钮。

如果所选专用连接设置支持配置 UI，而最终用户在 "**连接**" 选项卡中单击 "**配置**" 按钮，操作系统将调用连接属性扩展的 [**IDot11ExtUIProperty：:D isplaydot11extuiproperty**](/previous-versions/windows/hardware/wireless/ff553749(v=vs.85))方法来启动自定义 UI。 操作系统通过方法的 *bstrIHVProfile* 参数传递扩展插件的当前配置文件数据。

配置文件数据的格式为由 &lt; IHV &gt; &lt; /IHV &gt; XML 标记界定的 xml 片段。 这些标记中的 XML 数据特定于 IHV 的实现，对操作系统不透明。 有关本机802.11 配置文件数据格式的详细信息，请参阅 Microsoft Windows SDK 中的文档。

如果通过自定义 UI 更改了配置文件数据，则扩展的 [**IDot11ExtUIProperty：:D isplaydot11extuiproperty**](/previous-versions/windows/hardware/wireless/ff553749(v=vs.85)) 方法必须在返回前执行以下操作：

-   为修改后的配置文件数据分配字符串缓冲区，并通过方法的 *bstrModifiedIHVProfile* 参数返回指向缓冲区的指针。
    **注意**  扩展的 [**IDot11ExtUIProperty：:D isplaydot11extuiproperty**](/previous-versions/windows/hardware/wireless/ff553749(v=vs.85)) 方法不能修改 *bstrIHVProfile* 参数所引用的数据。

     

-   将 *pbIsModified* 参数设置为 **TRUE**。

 

 
