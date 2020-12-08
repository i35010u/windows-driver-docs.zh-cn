---
title: 通过 WIA 驱动程序创建和打开进程
description: 通过 WIA 驱动程序创建和打开进程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 937b78abd6fa7f22926cd8a4fa6771448ae532e7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824569"
---
# <a name="creating-and-opening-processes-by-wia-drivers"></a>通过 WIA 驱动程序创建和打开进程





WIA 驱动程序不应启动系统上的其他进程。 此操作的两个最重要的原因如下：

1.  调用 Microsoft Windows SDK 文档中所述的 **CreateProcess** () 会在启动该服务的同一帐户下启动进程。 在 Windows XP 中，这是 **LocalSystem** 帐户，这是一项重大安全风险。

2.  Windows SDK 文档中所述的 **CreateProcessAsUser** (在快速用户切换 (FUS) 或终端服务 (TS) 环境中) 可能会很困难。 在此级别上不正确地实现组件可以轻松地成功升级权限或信息泄露攻击。

**LocalService** 帐户没有足够的权限来启动其他进程。 因此，在 Microsoft Windows Server 2003 及更高版本上，WIA 驱动程序无法创建进程。

如果设备功能需要其他进程，则建议将其作为系统服务或本地 COM 服务器实现。 有关与创建系统服务和 COM 服务器相关的特定安全信息，请参阅 Microsoft 文档。

 

 




