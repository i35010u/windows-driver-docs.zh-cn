---
title: WIA 驱动程序的进程外 COM 对象
description: WIA 驱动程序的进程外 COM 对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 050f63c2a6b982dd7754804dfaacca7a172ab86c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841099"
---
# <a name="out-of-process-com-objects-for-wia-drivers"></a>WIA 驱动程序的进程外 COM 对象





如果驱动程序调用了 CoCreatInstance 组件的 Microsoft Windows SDK 文档) 中所述的 **CoCreatInstance** (，则此调用将失败，除非组件具有适当的权限集以允许访问驱动程序。

有关 COM 的安全模型的详细信息，请查阅 COM 编程书籍或联机文档。 下面是简短说明。

有两种与进程外 COM 组件相关联的权限：

-   启动权限

    启动权限指示哪些用户有权启动 COM 组件（如果当前未运行）。 例如，如果该组件是在未运行的本地服务器中实现的，则为该组件调用 **CoCreateInstance** 会导致 COM 尝试启动本地服务器 (假设调用方有权启动该服务器) 。

-   访问权限

    "访问权限" 指示允许哪些用户调用该进程，以检索这些 COM 组件的 COM 接口。

    启动权限和访问权限不一定要匹配。 例如，"启动" 权限只能设置为 "管理员"，但可将访问权限设置为 "交互式用户和管理员"。 或者，管理员可能被授予启动 COM 服务器的权限，但只有在 COM 服务器已经运行的情况下，普通用户才能使用这些组件。

一种很好的做法是将 COM 服务器的启动和访问权限存储在组件的 **AppId** 注册表子项下的适当位置。 这样，管理员就可以在需要时使用组件服务管理工具更改这些权限。 若要使您的 COM 服务器在运行时使用这些访问权限，请确保 Windows SDK 文档) 中所述的 **CoInitializeSecurity** (中所述的 EOAC \_ appid 标志，并传入组件的 **appid**。 这会导致 COM 在注册表中访问组件的 **AppId** 子项，并使用 **AccessPermission** 和 **LaunchPermission** 条目中的权限集。

 

 




