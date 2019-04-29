---
title: 将组件更改应用到注册表
description: 将组件更改应用到注册表
ms.assetid: f844a693-cf26-407c-b182-b652a4c585b4
keywords:
- 通知对象 WDK 网络、 注册表值
- 网络通知对象 WDK，注册表值
- 注册表 WDK 通知对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f170a0910b0067dd47b957d93e1b993d4d07458e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367708"
---
# <a name="applying-component-changes-to-the-registry"></a>将组件更改应用到注册表





在网络后配置子系统调用通知对象的[ **INetCfgComponentControl::ApplyRegistryChanges** ](https://msdn.microsoft.com/library/windows/hardware/ff547727)方法，通知对象应设置、 修改或删除中的信息根据通知对象由以前执行的操作的注册表。 通知对象执行与安装、 删除或修改参数，该对象所属的组件相关的特定操作后，通知对象应设置指示执行的操作的数据成员。 子系统调用后**ApplyRegistryChanges**配置更改应用于注册表**ApplyRegistryChanges**应使用此数据成员来确定如何进行注册表更改。 例如：

-   如果通知对象之前执行与安装该对象所属的组件相关的操作，通知对象应具有设置的数据成员的指示操作，如"安装"。 子系统调用后**ApplyRegistryChanges**配置更改应用于注册表**ApplyRegistryChanges**应在注册表中设置有关组件的信息。

-   如果通知对象之前执行与删除该对象所属的组件相关的操作，通知对象应具有设置的数据成员的指示操作，如"删除"。 子系统调用后**ApplyRegistryChanges**配置更改应用于注册表**ApplyRegistryChanges**应从注册表中删除有关组件的信息。

-   如果对象应具有设置的数据成员的用户显示其中一个组件的自定义属性页，并修改其中一个组件的参数，该组件通知，指示为"修改参数"的操作。 子系统调用后**ApplyRegistryChanges**配置更改应用于注册表**ApplyRegistryChanges**应更改注册表中的组件的参数有关的信息。

若要打开和检索组件的注册表项以修改该组件有关的信息**ApplyRegistryChanges**应实现方法以调用该组件[ **INetCfgComponent::OpenParamKey** ](https://msdn.microsoft.com/library/windows/hardware/ff547890)方法。 若要在组件的注册表项下的注册表中设置值，实现**ApplyRegistryChanges**编写使用 Win32 函数的注册表数据。 例如， **ApplyRegistryChanges**可以调用**RegCreateKeyEx**函数来创建一个子项来保存值，并且**RegSetValueEx**函数来创建并将这些设置值。

有关注册表的详细信息，写入数据，并检索数据，请参阅 Microsoft Windows SDK。

 

 





