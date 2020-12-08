---
title: 将组件更改应用到注册表
description: 将组件更改应用到注册表
keywords:
- 通知对象 WDK 网络，注册表值
- 网络通知对象 WDK，注册表值
- 注册表 WDK 通知对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f97ff7d73ce844eacc06552aa9953449ea79f148
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829991"
---
# <a name="applying-component-changes-to-the-registry"></a>将组件更改应用到注册表





网络配置子系统调用通知对象的 [**INetCfgComponentControl：： ApplyRegistryChanges**](/previous-versions/windows/hardware/network/ff547727(v=vs.85)) 方法之后，通知对象应根据通知对象先前执行的操作来设置、修改或删除注册表中的信息。 在 notify 对象执行特定操作（这些操作与安装、删除或修改拥有对象的组件的参数）相关后，"通知" 对象应设置指示所执行操作的数据成员。 在子系统调用 **ApplyRegistryChanges** 以将配置更改应用到注册表后， **ApplyRegistryChanges** 应该使用此数据成员来确定如何进行注册表更改。 例如：

-   如果通知对象先前执行了与安装拥有对象的组件相关的操作，则通知对象应将指示操作的数据成员设置为 "install"。 在子系统调用 **ApplyRegistryChanges** 以将配置更改应用到注册表后， **ApplyRegistryChanges** 应该在注册表中设置有关组件的信息。

-   如果通知对象先前执行了与删除拥有对象的组件相关的操作，则通知对象应将指示操作的数据成员设置为 "删除"。 在子系统调用 **ApplyRegistryChanges** 以将配置更改应用到注册表后， **ApplyRegistryChanges** 应从注册表中删除有关组件的信息。

-   如果用户显示某个组件的自定义属性页面并修改其中一个参数，则该组件的通知对象应将指示操作的数据成员设置为 "修改参数"。 在子系统调用 **ApplyRegistryChanges** 以将配置更改应用到注册表后， **ApplyRegistryChanges** 应更改注册表中有关该组件的参数的信息。

若要打开并检索组件的注册表项以修改有关组件的信息，应实现 **ApplyRegistryChanges** 方法以调用组件的 [**INetCfgComponent：： OpenParamKey**](/previous-versions/windows/hardware/network/ff547890(v=vs.85)) 方法。 若要在组件的注册表项下的注册表中设置值，请使用 Win32 函数实现 **ApplyRegistryChanges** 来写入注册表数据。 例如， **ApplyRegistryChanges** 可以调用 **RegCreateKeyEx** 函数来创建一个子项来保存值，使用 **RegSetValueEx** 函数创建和设置这些值。

有关注册表、向其中写入数据以及从中检索数据的详细信息，请参阅 Microsoft Windows SDK。

 

