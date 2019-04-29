---
title: 扩展无线连接属性
description: 扩展无线连接属性
ms.assetid: 77efa8f8-0b94-46b7-89d1-ec9c2c180845
keywords:
- IHV UI 扩展 DLL WDK 本机 802.11，无线连接属性
- 无线连接属性 WDK 本机 802.11 IHV UI 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b04c505fc8c572b2e24134ef4a33c8ec6525ab0e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386239"
---
# <a name="extending-wireless-connection-properties"></a>扩展无线连接属性




 

本主题介绍如何本机 802.11 IHV UI 扩展 DLL 上扩展属性**连接**显示通过网络配置用户界面 (UI) 选项卡。 在此情况下，本机 802.11 IHV UI 扩展 DLL 添加到的属性**连接**专有连接设置的选项卡。

有关网络配置 UI 和其他本机 802.11 组件的详细信息，请参阅[本机 802.11 软件体系结构](native-802-11-software-architecture.md)。

它显示之前**连接**选项卡上，操作系统执行以下操作：

1.  查询通过调用其连接属性的本机 802.11 IHV UI 扩展 DLL [ **IDot11ExtUI::GetDot11ExtUIProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff553776)方法。 操作系统将传递的值**DOT11\_EXT\_UI\_连接**给方法的*ExtType*参数。

    本机 802.11 IHV UI 扩展 DLL 是否支持类型的属性**DOT11\_EXT\_UI\_连接**，将返回该 DLL (通过该方法的*ppDot11ExtUIProperty*参数) 的地址[IDot11ExtUIProperty COM 接口](https://msdn.microsoft.com/library/windows/hardware/ff553746)，它可实现连接属性扩展。 有关用于扩展连接属性的 COM 接口的详细信息，请参阅[本机 802.11 IHV UI 扩展 COM 接口](native-802-11-ihv-ui-extensions-com-interfaces.md)。

    **请注意**  For Windows Vista 中，本机 802.11 IHV UI 扩展 DLL 不能返回多个[IDot11ExtUI COM 接口](https://msdn.microsoft.com/library/windows/hardware/ff553769)连接属性扩展。

     

2.  如果本机 802.11 IHV UI 扩展 DLL 支持连接属性，操作系统将通过调用扩展的查询的属性扩展的友好名称[ **IDot11ExtUIProperty::GetDot11ExtUIPropertyFriendlyName** ](https://msdn.microsoft.com/library/windows/hardware/ff553768)方法。 操作系统将插入的文本中的友好名称"启用*xxx*连接设置"位置"*xxx*"是属性扩展的友好名称。 操作系统上会显示此文本还提供了复选框**连接**选项卡。

3.  查询的扩展，以确定它是否有可以显示的自定义 UI 属性。 操作系统将这是通过调用扩展的[ **IDot11ExtUIProperty::Dot11ExtUIPropertyHasConfigurationUI** ](https://msdn.microsoft.com/library/windows/hardware/ff553756)方法。 如果连接属性扩展插件将支持自定义 UI 属性，操作系统将添加**配置**属性复选框下面的按钮。

如果所选的专有连接设置支持的配置 UI 和最终用户单击**配置**按钮**连接**选项卡上，操作系统将调用连接属性扩展的[ **IDot11ExtUIProperty::DisplayDot11ExtUIProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff553749)方法来启动自定义用户界面。 操作系统通过该方法的传递扩展插件的当前配置文件数据*bstrIHVProfile*参数。

配置文件数据的格式为 XML 片段受&lt;IHV&gt; &lt;/IHV&gt; XML 标记。 在此标记中的 XML 数据是特定于 IHV 的实现，并对操作系统是不透明。 本机 802.11 配置文件数据的格式的详细信息，请参阅 Microsoft Windows SDK 中的文档。

如果更改自定义 UI，该扩展的运行配置文件数据[ **IDot11ExtUIProperty::DisplayDot11ExtUIProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff553749)方法必须执行以下操作在返回之前：

-   修改后的配置文件数据分配一个字符串缓冲区并通过该方法的返回指向缓冲区的指针*bstrModifiedIHVProfile*参数。
    **请注意**  扩展的[ **IDot11ExtUIProperty::DisplayDot11ExtUIProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff553749)方法不能修改引用的数据*bstrIHVProfile*参数。

     

-   设置*pbIsModified*自变量**TRUE**。

 

 





