---
title: V4 打印机驱动程序的用户界面
description: V4 打印驱动程序支持 Windows 桌面 UI 和 Microsoft Store 应用程序 UI 中的自定义项。
ms.assetid: DE45C0F3-3385-451D-AD29-94D28089E9C3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c774c757e963a48393d22a7b36421ea88d042a60
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547015"
---
# <a name="v4-printer-driver-user-interfaces"></a>V4 打印机驱动程序的用户界面


V4 打印驱动程序支持 Windows 桌面 UI 和 Microsoft Store 应用程序 UI 中的自定义项。

由于这些体验截然不同性质，这些 Ui 必须实现为两个不同的应用程序。 但是，同时配置模块提供常见的 COM API 为基础构建。 打印机扩展在 desktop 中支持 v4 打印驱动程序和使用所有现有应用程序。 和打印机扩展也适用于打印机共享与增强的指向和打印驱动程序的方案。 适用于所有操作系统从 Windows Vista 通过 Windows 8 计划支持。

UWP 的设备应用程序支持 Microsoft Store 应用程序 UI 中的 v4 打印驱动程序。 有关开发 UWP 设备应用程序的详细信息，请参阅[开发 UWP 设备应用用于打印](https://msdn.microsoft.com/library/windows/hardware/br259129.aspx)。

下图显示了自定义的 Ui 和打印系统之间的通信体系结构的高级别概述。

![自定义 ui 和打印系统通信的高级别概述](images/v4customuicomms.png)

下面的主题提供有关用户界面的更详细地了解在 v4 打印驱动程序的支持。

[V4 驱动程序 UI 体系结构](v4-driver-ui-architecture.md)

[自定义 UI 的驱动程序支持](driver-support-for-customized-ui.md)

[作业管理](job-management.md)

[设备维护](device-maintenance.md)

[打印机扩展](printer-extensions.md)

[UWP 应用的打印机的设备应用程序](uwp-device-apps-for-printers.md)

## <a name="related-topics"></a>相关主题
[V4 打印机驱动程序](v4-printer-driver.md)  



