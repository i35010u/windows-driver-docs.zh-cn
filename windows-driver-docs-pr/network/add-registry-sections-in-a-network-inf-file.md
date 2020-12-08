---
title: 网络 INF 文件中的 Add-registry-sections
description: 网络 INF 文件中的 Add-registry-sections
keywords:
- INF 文件 WDK 网络，添加注册表部分
- 网络 INF 文件 WDK，添加-注册表-部分
- 添加-注册表-部分 WDK 网络
- 添加-注册表-有关 WDK 网络的信息，有关外接程序的部分
- 密钥 WDK 网络 INF 文件
- Ndi 密钥 WDK 网络
- 值 WDK 网络 INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74aa2161bc0aed975df330e70dac53f1706adbe4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799435"
---
# <a name="add-registry-sections-in-a-network-inf-file"></a>网络 INF 文件中的 Add-registry-sections





INF 文件包含安装的每个组件的一个或多个 " *添加注册表" 部分* 。 " *添加注册表" 部分* 会向注册表中添加键和值。 INF 文件的 **DDInstall** 部分包含引用一个或多个 *添加注册表部分* 的 **AddReg** 指令。 有关 " *添加注册表" 部分* 和 " **AddReg** " 指令的详细信息，请参阅 [**INF AddReg 指令**](../install/inf-addreg-directive.md)。

### <a name="adding-keys-and-values-to-instance-keys"></a>将键和值添加到实例键

一个或多个 *添加注册表部分* 可以向组件的实例键添加键和值，以完成以下任一操作：

-   为组件设置静态参数-即，无法通过用户界面修改的配置参数。 有关详细信息，请参阅 [设置静态参数](setting-static-parameters.md)。

-   指定 WAN 适配器)  (也称为通道、线路或持有者通道的终结点数。 有关详细信息，请参阅为 [Wan 适配器指定 Wan 终结点](specifying-wan-endpoints-for-a-wan-adapter.md)。

-   指定 ISDN 适配器的密钥和值。 有关详细信息，请参阅为 [Isdn 适配器指定 Isdn 密钥和值](specifying-isdn-keys-and-values-for-an-isdn-adapter.md)。

-   需要安装其他网络组件。 有关详细信息，请参阅 [要求安装其他网络组件](requiring-the-installation-of-another-network-component.md)。

-   指定支持网络适配器的自定义属性表的值。 有关详细信息，请参阅为 [网络适配器指定自定义属性页](specifying-custom-property-pages-for-network-adapters.md)。

### <a name="adding-keys-and-values-to-a-netclient-component"></a>向 NetClient 组件添加键和值

**NetClient** 组件的 INF 文件中的 "*添加注册表" 部分* 必须将 **NetworkProvider** 键添加到该组件的 *服务* 密钥。 **NetworkProvider** 键具有两个值：指定网络提供程序的名称的 **名称**，以及指定网络提供程序 DLL 的完整路径的 **ProviderPath** 。 有关详细信息，请参阅 [指定 NetClient 组件的名称和提供程序路径](specifying-the-name-and-provider-path-for-a-netclient-component.md)。

**请注意**，**NetClient** 组件在 Windows 8.1、Windows Server 2012 R2 和更高版本中已弃用。  

 

### <a name="creating-the-ndi-key"></a><a href="" id="ddk-creating-the-ndi-key-ng"></a>创建 Ndi 键

每个网络 INF 文件必须至少包含一个 " *添加注册表" 部分* ，该部分会为文件所安装的组件添加 **Ndi** 密钥。 **Ndi** 键是一个网络特定的密钥，它添加到组件的实例键。 添加到 **Ndi** 项的键和值因要安装的网络组件类型及其功能而异。 **Ndi** 项指定以下内容：

-   **NetTrans**、 **NetClient** 或 **空间** 组件的 **HelpText** 值。 有关详细信息，请参阅 [添加 HelpText 值](adding-a-helptext-value.md)。

-   通知对象的值。 有关详细信息，请参阅 [添加通知对象的注册表值](adding-registry-values-for-a-notify-object.md)。

-   与服务相关的值。 有关详细信息，请参阅 [将 Service-Related 值添加到 Ndi 项](adding-service-related-values-to-the-ndi-key.md)。

-   绑定接口。 有关详细信息，请参阅 [指定绑定接口](specifying-binding-interfaces.md)。

-   " **高级** " 页的适配器配置参数。 有关详细信息，请参阅 [指定高级属性页的配置参数](specifying-configuration-parameters-for-the-advanced-properties-page.md)。

-   绑定成员身份。 有关详细信息，请参阅 [指定绑定成员身份](specifying-bundle-membership.md)。

有关 windows 95/98/Me 中提供但未在 Windows 2000 和更高版本中使用的 **Ndi** 注册表项和值的列表，请参阅 [Windows 2000 及更高版本中未使用的 Ndi 值和键](ndi-values-and-keys-not-used-in-windows-2000-and-later-versions.md)。

 

