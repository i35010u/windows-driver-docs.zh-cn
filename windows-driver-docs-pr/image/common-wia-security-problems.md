---
title: 常见的 WIA 安全问题
description: 常见的 WIA 安全问题
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 783c9c73c4c09387cd56a3b100c47ce3e899a9c5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823179"
---
# <a name="common-wia-security-problems"></a>常见的 WIA 安全问题





有几个常见问题会阻止现有的 WIA 驱动程序 (在 **LocalSystem** 下运行良好的 WIA 驱动程序) 在 **LocalService** 帐户下成功运行。

最常见的问题出现在：

-   文件系统访问

    **LocalService** 帐户具有严格限制的文件访问权限。 例如，驱动程序不能再写入%*windir*% 目录。

-   注册表访问

    许多打开到 **LocalSystem** 帐户的注册表项对于 **LocalService** 是只读的。 例如，驱动程序将无法再写入 HKLM 子树下的注册表项。

-   命名的内核对象

    请确保已命名的对象 (例如，WIA 驱动程序和外部组件（例如捆绑的应用程序）访问的事件和互斥) 体具有相应的 Acl。 如果某个应用程序创建一个命名的事件对象，但未明确授予对 **LocalService** 帐户的访问权限，则该驱动程序将无法使用它。 同样，如果微型驱动程序创建命名的事件对象，则它必须授予相同的访问权限，否则应用程序将不能使用事件对象。

-   进程外 COM 对象

    任何创建或使用进程外 COM 接口的尝试都将失败，除非该组件显式向 **LocalService** 帐户授予适当的权限。 例如， **CoCreateInstance** **CoCreateInstanceEx** \_ \_ 如果组件未向 **LocalService** 帐户授予权限，则 Microsoft Windows SDK 文档) 中描述了对 CoCreateInstance 或 CoCreateInstanceEx (两者的调用。 同样，尝试使用指向驱动程序的 COM 接口的指针的驱动程序可能会失败。 如果组件调用了驱动程序，并向其传递一个指向接口的指针，驱动程序可以回调接口，则会发生这种情况。

-   创建和打开进程

    WIA 驱动程序不应手动启动其他进程 (例如，通过调用 **CreateProcess** 或 **CreateProcessAsUser**) 。 尽管此行为对于 **LocalSystem** 帐户下的驱动程序已成功完成，但在新的 **LocalService** 帐户下，驱动程序不能再执行此操作。 有关 **CreateProcess** 和 **CreateProcessAsUser** 的详细信息，请参阅 Windows SDK 文档。

 

 




