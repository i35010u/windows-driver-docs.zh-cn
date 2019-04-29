---
title: WIA 驱动程序的进程外 COM 对象
description: WIA 驱动程序的进程外 COM 对象
ms.assetid: 0b08652e-36ae-46f8-8915-7f2bb45df05c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24f0ff71301ac85c706fee138727ddb17aa526a2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392624"
---
# <a name="out-of-process-com-objects-for-wia-drivers"></a>WIA 驱动程序的进程外 COM 对象





如果驱动程序调用**CoCreatInstance** （Microsoft Windows SDK 文档中所述） 上的进程外组件，调用将失败，除非该组件具有适当的权限设置为允许驱动程序访问。

有关 COM 的安全模型的详细信息，请查阅 COM 编程书籍或联机文档。 下面是简要说明。

有两种类型的进程外 COM 组件与关联的权限：

-   启动权限

    启动权限将指示谁有权启动 COM 组件，如果当前未运行。 例如，如果在未运行的本地服务器中实施该组件，则调用**CoCreateInstance**为该组件结果在 COM 中尝试启动本地服务器 （假定调用方有权启动它）。

-   访问权限

    访问权限将指示谁有权调用该过程以检索这些 COM 组件的 COM 接口。

    启动权限和访问权限不需要匹配。 例如，启动权限可能被设置为管理员，但无法向交互式用户和管理员设置访问权限。 或者，管理员可能会授予权限以启动 COM 服务器，但一般用户将仅能使用的组件，如果已经运行了 COM 服务器。

较好的做法是在下的组件的适当位置中存储的 COM 服务器启动和访问权限**AppId**注册表子项。 这样，管理员可以更改这些权限，如果需要请使用组件服务管理工具。 若要使您在运行时使用这些访问权限的 COM 服务器，请务必调用**CoInitializeSecurity** （Windows SDK 文档中所述） 与 EOAC\_APPID 标志，在组件的传递**AppId**。 这将导致以转到该组件的 COM **AppId**子项的注册表中和使用中设置的权限**AccessPermission**并**LaunchPermission**条目。

 

 




