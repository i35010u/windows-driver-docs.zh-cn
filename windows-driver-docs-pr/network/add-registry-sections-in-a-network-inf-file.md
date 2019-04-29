---
title: 网络 INF 文件中的 Add-registry-sections
description: 网络 INF 文件中的 Add-registry-sections
ms.assetid: 43c39389-5d01-49e9-a792-e853136068b4
keywords:
- INF 文件 WDK 网络，添加注册表部分
- 可使用网络 INF 文件 WDK，添加注册表部分
- 添加注册表部分 WDK 网络
- 有关添加注册表部分添加注册表部分 WDK 网络
- 密钥 WDK 网络 INF 文件
- Ndi 密钥 WDK 网络
- 值 WDK 网络 INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce91eca10d49e0b3dfdcd8a3f87f2eadb2825387
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367793"
---
# <a name="add-registry-sections-in-a-network-inf-file"></a>网络 INF 文件中的 Add-registry-sections





INF 文件包含一个或多个*添加注册表部分*为每个组件的安装。 *添加注册表部分*将键和值添加到注册表。 **DDInstall** INF 文件部分包含**AddReg**指令，它引用一个或多个*添加注册表部分*。 有关详细信息*添加注册表部分*并**AddReg**指令，请参阅[ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)。

### <a name="adding-keys-and-values-to-instance-keys"></a>将键和值添加到的实例键

一个或多个*添加注册表部分*可以将键和值添加到组件来完成以下任一实例键：

-   设置静态参数的组件-即，不能通过用户界面修改的配置参数。 有关详细信息，请参阅[设置的静态参数](setting-static-parameters.md)。

-   指定 WAN 适配器终结点 （也称为通道、 线路或持有者渠道） 数量。 有关详细信息，请参阅[WAN 适配器指定 WAN 终结点](specifying-wan-endpoints-for-a-wan-adapter.md)。

-   指定键和 ISDN 适配器的值。 有关详细信息，请参阅[指定 ISDN 键和值的 ISDN 适配器](specifying-isdn-keys-and-values-for-an-isdn-adapter.md)。

-   需要另一个网络组件的安装。 有关详细信息，请参阅[需要安装的另一个网络组件](requiring-the-installation-of-another-network-component.md)。

-   指定的网络适配器支持的自定义属性表的值。 有关详细信息，请参阅[的自定义属性页指定网络适配器](specifying-custom-property-pages-for-network-adapters.md)。

### <a name="adding-keys-and-values-to-a-netclient-component"></a>将键和值添加到 NetClient 组件

*添加注册表部分*INF 文件，用于**NetClient**组件必须添加**NetworkProvider**关键*服务*密钥对的组件。 **NetworkProvider**密钥有两个值：**名称**指定的网络提供商，名称和一个**ProviderPath** ，它指定到网络的完整路径提供程序 DLL。 有关详细信息，请参阅[NetClient 组件的指定名称和提供程序路径](specifying-the-name-and-provider-path-for-a-netclient-component.md)。

**请注意**  **NetClient**组件在 Windows 8.1，Windows Server 2012 R2 中已弃用及更高版本。

 

### <a href="" id="ddk-creating-the-ndi-key-ng"></a>创建 Ndi 密钥

每个网络 INF 文件必须包含至少一个*添加注册表部分*，它将**Ndi**密钥对该文件由安装的组件。 **Ndi**密钥是特定于网络的密钥添加到组件的实例键。 键和值添加到**Ndi**密钥正在安装的网络组件和及其功能的类型而异。 **Ndi**项指定以下：

-   **HelpText**值**NetTrans**， **NetClient**，或**NetService**组件。 有关详细信息，请参阅[添加 HelpText 值](adding-a-helptext-value.md)。

-   通知对象的值。 有关详细信息，请参阅[的通知对象添加注册表值](adding-registry-values-for-a-notify-object.md)。

-   与服务相关的值。 有关详细信息，请参阅[Adding Service-Related 值到 Ndi 密钥](adding-service-related-values-to-the-ndi-key.md)。

-   绑定接口。 有关详细信息，请参阅[指定绑定接口](specifying-binding-interfaces.md)。

-   适配器的配置参数**高级**页。 有关详细信息，请参阅[的高级属性页指定配置参数](specifying-configuration-parameters-for-the-advanced-properties-page.md)。

-   捆绑包的成员身份。 有关详细信息，请参阅[指定捆绑包成员资格](specifying-bundle-membership.md)。

有关一系列**Ndi**注册表项和值是在 Windows 95/98/我可用，但不是使用在 Windows 2000 和更高版本，请参阅[Ndi 值和在 Windows 2000 和更高版本中不使用密钥](ndi-values-and-keys-not-used-in-windows-2000-and-later-versions.md)。

 

 





