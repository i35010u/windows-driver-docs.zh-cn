---
title: WIA 驱动程序的命名空间
description: WIA 驱动程序的命名空间
ms.assetid: 67260a25-6233-4738-a08f-26223cc8e563
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9411744e22d6073a7f6d9a7ae18017144845b10e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379659"
---
# <a name="namespaces-for-wia-drivers"></a>WIA 驱动程序的命名空间





在会话 0 中运行所有服务。 但是，可能在不同会话中运行应用程序。 每个会话都有自己*命名空间*。 因此，在一个会话中创建的命名的对象通常将看不到组件在其他会话中。

此问题的解决方案是确保这两个组件使用相同的命名空间。 若要执行此操作的最简单方法是使用*全局命名空间*。 例如，如果捆绑的组件访问外部 WIA 的设备，它可能会使用名为的互斥体对象**MyDeviceLock**其 WIA 的驱动程序与同步访问。 若要将互斥体名称放在全局命名空间，它应调用**Global\\MyDeviceLock**。 名为 mutex **Global\\MyDeviceLock**对驱动程序和应用程序，无论哪个会话正在中运行，因为它们都指定属于全局命名空间的名称是可见的。

在 Microsoft Windows SDK 文档了解详细信息，请参阅"内核对象命名空间"。

 

 




