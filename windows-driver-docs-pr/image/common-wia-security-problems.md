---
title: 常见的 WIA 安全问题
description: 常见的 WIA 安全问题
ms.assetid: d3f7d6e9-1ac4-4209-92bb-d08e4e13a4ad
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc9c2b087f16b71f8a59f5f570a2dd1110d98e5e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373203"
---
# <a name="common-wia-security-problems"></a>常见的 WIA 安全问题





有几个常见的问题可能会阻止现有 WIA 驱动程序 (其运行下可正常**LocalSystem**) 从运行已成功在**LocalService**帐户。

使用发生最常见的问题：

-   文件系统访问权限

    **LocalService**帐户具有严格的限制文件访问权限。 例如，驱动程序可以不能再写入到 %*windir*%目录。

-   注册表访问

    很多，到打开了的注册表项**LocalSystem**帐户是对只读**LocalService**。 例如，驱动程序将不再能够写入到 HKLM 子树下的注册表项。

-   命名的内核对象

    请确保具有适当的 Acl 的名为 WIA 驱动程序和外部组件，例如捆绑应用程序访问的对象 （例如，事件和互斥锁）。 如果应用程序创建一个命名的事件对象，但不会专门授予访问**LocalService**帐户，该驱动程序将无法再使用它。 同样，如果微型驱动程序创建一个命名的事件对象，它必须授予相同的访问权限或应用程序将无法再使用事件对象。

-   进程外 COM 对象

    创建或使用进程外 COM 接口的任何尝试将失败，除非该组件显式授予适当的权限**LocalService**帐户。 例如，调用**CoCreateInstance**或**CoCreateInstanceEx** （同时描述了 Microsoft Windows SDK 文档中） 使用 CLSCTX\_本地\_服务器标志如果该组件不会授予权限集可能会失败**LocalService**帐户。 同样，尝试使用不是过程向驱动程序的 COM 接口指针的驱动程序可能会失败。 如果一个组件调用驱动程序，并将其指针的驱动程序可回调接口的接口，这可能发生。

-   创建和打开进程

    WIA 驱动程序不应手动启动其他进程 (例如，通过调用**CreateProcess**或**CreateProcessAsUser**)。 尽管此行为将会成功的驱动程序下**LocalSystem**帐户，就不能再为此，在新的驱动程序可能**LocalService**帐户。 有关详细信息**CreateProcess**并**CreateProcessAsUser**，请参阅 Windows SDK 文档。

 

 




