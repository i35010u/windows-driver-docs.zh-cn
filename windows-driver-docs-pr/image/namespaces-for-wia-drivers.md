---
title: WIA 驱动程序的命名空间
description: WIA 驱动程序的命名空间
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83126e1e8d4a6cd18a4b8edd26b07c5294d99722
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827107"
---
# <a name="namespaces-for-wia-drivers"></a>WIA 驱动程序的命名空间





所有服务都在会话0中运行。 但是，应用程序可能在不同的会话中运行。 每个会话都有自己的 *命名空间*。 因此，在一个会话中创建的命名对象通常不会对其他会话中的组件可见。

此问题的解决方法是确保这两个组件使用同一个命名空间。 执行此操作的最简单方法是使用 *全局命名空间*。 例如，如果捆绑的组件在 WIA 之外访问设备，则可能使用名为 **MyDeviceLock** 的 mutex 对象将访问权限与 wia 驱动程序同步。 若要将 mutex 名称放在全局命名空间中，应将其称为 **global \\ MyDeviceLock**。 命名为 **Global \\ MyDeviceLock** 的 mutex 对驱动程序和应用程序都可见，无论它们在哪个会话中运行，因为它们都指定该名称属于全局命名空间。

有关详细信息，请参阅 Microsoft Windows SDK 文档中的 "内核对象命名空间"。

 

 




