---
title: MB 设备服务
description: Windows 7 引入了 NDIS (网络设备接口规范基于) 的驱动程序模型，以支持移动宽带 (MB) 设备。
ms.assetid: 7F9DFD96-2221-4F64-AC51-F336CCBED6BF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d45bcbda8b826963e26e894f6902fff0d7425d96
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733939"
---
# <a name="mb-device-services"></a>MB 设备服务


Windows 7 引入了 NDIS (网络设备接口规范基于) 的驱动程序模型，以支持移动宽带 (MB) 设备。 Windows 8 展开了模型，以便为基于 USB 的移动宽带设备实现标准化的硬件接口。 此硬件接口规范称为移动宽带接口模型 (MBIM) 。

Windows 8 提供了一个适用于符合 MBIM 规范的设备的已更新类驱动程序。 此模型称为 MB 类驱动程序。 但是，没有类驱动程序可以支持 MB 设备公开的所有功能。 为了允许 IHV 合作伙伴继续创新，MB 类驱动程序提供了一种机制，如 [**IMbnDeviceService 接口**](/windows/win32/api/mbnapi/nn-mbnapi-imbndeviceservice) ，以允许 ihv 扩展类驱动程序功能的行为。

**注意**   扩展 MB 设备服务的功能通过用户模式应用程序完成，而不是内核模式驱动程序扩展。

 

虽然 Windows 7 中引入的类驱动程序具有有限 MB 的设备功能支持，但 Windows 8 中的 MB 类驱动程序添加了对某些附加功能（例如 USSD、EAP-SIM/和 USB 选择性挂起）的本机支持，并提供了可扩展的设备表示形式和控制机制。 [移动宽带 WINRT API 概述](../mobilebroadband/list-of-mobile-broadband-windows-runtime-apis.md)提供了一些有关扩展设备服务的其他信息。

Windows 8 中的 MB 类驱动程序使纵向解决方案提供商可以使用 [移动宽带 API 接口](/windows/desktop/mbn/mobile-broadband-networks-api-interfaces) 来创建 Windows 以外的增强型用户体验。 扩展机制是一种补充（而不是替换） MB 类驱动程序中支持的功能的方法。 例如，IHV 可以提供特定于供应商的软件，在设备上执行固件更新。 或者，IHV 可以提供特定于供应商的软件，该软件提供了值添加服务，例如 SIM 工具包 (STK) 或电话簿。 [Appcontainer mobile 宽带 pin、连接和管理](/samples/browse/)示例演示了 appcontainer 中用于访问和管理移动宽带功能的 WIN32/COM 移动宽带 api。

除了提供扩展 MB 类驱动程序功能的机制外，Windows 还提供了一些机制，使 Ihv 可以通过 Windows 更新 (WU) 部署和安装其增值软件。

有关详细信息，请参阅：

-   移动宽带接口模型的 "MBIM 服务和 CID 扩展性" 部分 [ (MBIM) 规范]( https://go.microsoft.com/fwlink/p/?linkid=320791)

