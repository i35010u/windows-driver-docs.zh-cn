---
title: V4 打印机驱动程序用户界面
description: V4 打印驱动程序支持 Windows 桌面 UI 和 Microsoft Store 应用 UI 中的自定义。
ms.assetid: DE45C0F3-3385-451D-AD29-94D28089E9C3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c8bd83dd13d16e8809be026767fe852e59eec18
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211901"
---
# <a name="v4-printer-driver-user-interfaces"></a>V4 打印机驱动程序用户界面


V4 打印驱动程序支持 Windows 桌面 UI 和 Microsoft Store 应用 UI 中的自定义。

由于这些经验的性质，必须将这些 Ui 实现为两个不同的应用程序。 但是，这两种方法都是基于配置模块提供的通用 COM API 构建的。 打印机扩展在桌面中支持 v4 打印驱动程序，并使用所有现有的应用程序。 打印机扩展还适用于带有增强点和打印驱动程序的打印机共享方案。 针对 Windows Vista 到 Windows 8 中的所有操作系统计划支持。

UWP 设备应用在 Microsoft Store 应用 UI 中支持 v4 打印驱动程序。 有关开发 UWP 设备应用的详细信息，请参阅 [开发 uwp 设备应用以进行打印](../devapps/uwp-device-apps-for-printers.md)。

下图显示了自定义 Ui 和打印系统之间的通信体系结构的高级概述。

![自定义 ui 和打印系统通信的高级概述](images/v4customuicomms.png)

以下主题更详细地介绍了 v4 打印驱动程序对用户界面的支持。

[V4 驱动程序 UI 体系结构](v4-driver-ui-architecture.md)

[自定义 UI 的驱动程序支持](driver-support-for-customized-ui.md)

[作业管理](job-management.md)

[设备维护](device-maintenance.md)

[打印机扩展](printer-extensions.md)

[适用于打印机的 UWP 设备应用](uwp-device-apps-for-printers.md)

## <a name="related-topics"></a>相关主题
[v4 打印机驱动程序](v4-printer-driver.md)