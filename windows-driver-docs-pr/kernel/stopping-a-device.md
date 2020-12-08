---
title: 停止设备
description: 停止设备
keywords:
- PnP WDK 内核，停止设备
- 即插即用 WDK 内核，停止设备
- 停止 PnP 设备
- 停止 Irp WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f380038242cb8de5dbc7943b3b77cf66ccb4b94
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814285"
---
# <a name="stopping-a-device"></a>停止设备





PnP 管理器指示驱动程序在以下情况下停止设备：

-   重新平衡设备使用的硬件资源。 当枚举的新设备需要已使用的资源时，通常需要重新平衡。

-   若要禁用设备以响应设备管理器请求 (Windows 98/Me 只) 。 在这种情况下，windows 2000 和更高版本的 Windows 发送删除 Irp;请参阅 [了解何时发出删除 irp](understanding-when-remove-irps-are-issued.md)。

-   失败后， [**IRP \_ MN \_ 启动 \_ 设备**](./irp-mn-start-device.md) 请求 (仅限 Windows 98/Me) 

本部分涵盖了以下主题：

[停止设备以重新平衡资源](stopping-a-device-to-rebalance-resources.md)

[停止设备以将其禁用 (Windows 98/Me)](stopping-a-device-to-disable-it--windows-98-me-.md)

[启动失败后停止设备 (Windows 98/Me)](stopping-a-device-after-a-failed-start--windows-98-me-.md)

[处理停止 IRP（Windows 2000 和更高版本）](handling-stop-irps--windows-2000-and-later-.md)


 

