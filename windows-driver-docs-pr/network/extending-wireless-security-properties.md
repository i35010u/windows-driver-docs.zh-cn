---
title: 扩展无线安全属性
description: 扩展无线安全属性
ms.assetid: be6af188-fa60-4ac8-a699-97a3baaec6be
keywords:
- IHV UI 扩展 DLL WDK 本机 802.11，安全属性
- 安全属性 WDK 本机 802.11 IHV UI 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49c9ad86cb3185d24e3d1df13bb29c9c9bd079d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347416"
---
# <a name="extending-wireless-security-properties"></a>扩展无线安全属性




 

本主题介绍如何本机 802.11 IHV UI 扩展 DLL 扩展的属性**安全**显示通过网络配置用户界面 (UI) 选项卡。 在此情况下，本机 802.11 IHV UI 扩展 DLL 添加到的属性**安全**是互斥的本机 802.11 802.1x 模块中的专用安全设置的选项卡。

本机 802.11 IHV UI 扩展 DLL 还可以扩展本机 802.11 802.1x 模块支持的安全和加密方法。 有关 DLL 如何执行此详细信息，请参阅[扩展 Microsoft 802.1 X 安全设置](extending-microsoft-802-1x-security-settings.md)。

有关网络配置 UI 和其他本机 802.11 组件的详细信息，请参阅[本机 802.11 软件体系结构](native-802-11-software-architecture.md)。

它显示之前**安全**选项卡上，操作系统执行以下操作：

1.  查询通过调用其安全属性扩展的本机 802.11 IHV UI 扩展 DLL [ **IDot11ExtUI::GetDot11ExtUIProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff553776)方法。 操作系统将传递的值**DOT11\_EXT\_UI\_安全**给方法的*ExtType*参数。

    如果本机 802.11 IHV UI 扩展 DLL 支持类型的一个或多个属性**DOT11\_EXT\_UI\_安全**，将返回该 DLL (通过该方法的*ppDot11ExtUIProperty*参数) 的列表[IDot11ExtUIProperty COM 接口](https://msdn.microsoft.com/library/windows/hardware/ff553746)支持 DLL 的安全属性扩展的。 有关用来扩展安全属性的 COM 接口的详细信息，请参阅[本机 802.11 IHV UI 扩展 COM 接口](native-802-11-ihv-ui-extensions-com-interfaces.md)。

2.  通过调用扩展的查询的安全扩展插件的友好名称[ **IDot11ExtUIProperty::GetDot11ExtUIPropertyFriendlyName** ](https://msdn.microsoft.com/library/windows/hardware/ff553768)方法。 操作系统将友好名称添加到列表底部的专有的安全设置**安全**选项卡。

3.  如果最终用户从该列表中选择某个项，操作系统将调用[ **IDot11ExtUIProperty::Dot11ExtUIPropertyGetSelected** ](https://msdn.microsoft.com/library/windows/hardware/ff553753)方法的每个安全扩展插件的[IDot11ExtUIProperty COM 接口](https://msdn.microsoft.com/library/windows/hardware/ff553746)。 返回的值的第一个扩展 **，则返回 TRUE**方法的*pfIsSelected*参数被确定为所选的扩展。 然后将突出显示列表中的所选的条目。

4.  查询所选的设置[ **IDot11ExtUIProperty::Dot11ExtUIPropertyHasConfigurationUI** ](https://msdn.microsoft.com/library/windows/hardware/ff553756)方法，以确定是否有可以显示的自定义 UI 属性页面。 如果该方法返回与*fHasConfigurationUI*参数设置为**TRUE**，将添加操作系统**配置**专用安全列表旁的按钮设置。

如果选择专有的安全设置支持的配置 UI 和最终用户单击**配置**按钮，操作系统将调用的设置[ **IDot11ExtUIProperty::DisplayDot11ExtUIProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff553749)方法来启动自定义用户界面。 操作系统通过方法将当前的配置文件数据传递设置*bstrIHVProfile*参数。

配置文件数据的格式为 XML 片段受&lt;IHV&gt; &lt;/IHV&gt; XML 标记。 在此标记中的 XML 数据是特定于 IHV 的实现，并对操作系统是不透明。 本机 802.11 配置文件数据的格式的详细信息，请参阅 Microsoft Windows SDK 中的文档。

如果通过自定义用户界面，该设置的更改的配置文件数据[ **IDot11ExtUIProperty::DisplayDot11ExtUIProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff553749)方法必须执行以下操作在返回之前：

-   修改后的配置文件数据分配一个字符串缓冲区并通过该方法的返回指向缓冲区的指针*bstrModifiedIHVProfile*参数。
    **请注意**  的设置[ **IDot11ExtUIProperty::DisplayDot11ExtUIProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff553749)方法不能修改引用的数据*bstrIHVProfile*参数。

     

-   设置*pbIsModified*自变量**TRUE**。

 

 





