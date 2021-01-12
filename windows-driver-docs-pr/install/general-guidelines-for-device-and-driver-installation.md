---
title: 设备和驱动程序安装常规指南
description: 设备和驱动程序安装常规指南
keywords:
- 设备安装 WDK，一般指导原则
- 驱动程序安装 WDK，一般指导原则
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ebb8826e82a4135e2b9dcbc00833159d429bb13
ms.sourcegitcommit: 10fecd036370f5eccb538004c5bec1fdd18c3275
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "98124141"
---
# <a name="general-guidelines-for-device-and-driver-installation"></a>设备和驱动程序安装常规指南


在 Windows 操作系统上安装设备和驱动程序的基本目标是尽可能使用户尽可能轻松地完成此过程。 安装过程和 [驱动程序包](driver-packages.md) 的组件应与操作系统的 [设备安装组件](/previous-versions/ff541277(v=vs.85))无缝配合使用。

若要提供最佳的用户体验，请使用以下准则来设计和实现你的安装过程：

-   除非绝对必要，否则不要自动重新启动系统或要求用户执行此操作。

-   始终使用 [INF 文件](overview-of-inf-files.md) 进行设备安装。 请确保所有 INF 文件的格式正确并使用正确的语法。

-   安装后在系统上保留 INF 文件;不要删除它们。 INF 文件不仅在第一次安装设备或驱动程序时使用，还在用户通过设备管理器请求驱动程序更新时使用。

-   使用 [系统定义的设备安装程序类](./system-defined-device-setup-classes-reserved-for-system-use.md)之一。 除非有很有说服力的原因，否则不要定义自己的安装类。

-   不要对注册表项或值的位置、格式或含义做出假设。 有关注册表项和树的详细信息，请参阅 [设备和驱动程序的注册表树和密钥](registry-trees-and-keys.md)。

