---
title: 创建和打开 WIA 驱动程序的进程
description: 创建和打开 WIA 驱动程序的进程
ms.assetid: c939eb25-b92b-41ef-ade0-98c2a707fee6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab761149b2a01f55254b8fbc35feed1006842ea1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524539"
---
# <a name="creating-and-opening-processes-by-wia-drivers"></a>创建和打开 WIA 驱动程序的进程





WIA 驱动程序不应在系统上启动其他进程。 有关这两个最重要的原因如下所示：

1.  调用**CreateProcess** （Microsoft Windows SDK 文档中所述） 启动在其中启动该服务在同一帐户下的过程。 在 Windows XP 中，这是**LocalSystem**帐户，这是重大安全风险。

2.  调用**CreateProcessAsUser** （Windows SDK 文档中所述） 很难快速用户切换 (FUS) 或终端服务 (TS) 环境中。 不正确的权限或信息泄露攻击成功升级可以轻松地会导致此级别的实现的组件。

**LocalService**帐户没有足够的特权启动其他进程。 因此，Microsoft Windows Server 2003 及更高版本，WIA 驱动程序无法创建进程。

如果设备功能需要另一个进程，则建议，它作为系统服务或本地 COM 服务器实现。 请参阅特定的安全信息与创建的系统服务和 COM 服务器相关的 Microsoft 文档。

 

 




