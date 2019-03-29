---
title: MB 设备服务
description: Windows 7 引入了用于支持移动宽带 (MB) 设备的 NDIS （网络设备接口规范） 基于驱动程序模型。
ms.assetid: 7F9DFD96-2221-4F64-AC51-F336CCBED6BF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f9e1b26cf1dd3d64c901f5ad18eebc5a3755760
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567638"
---
# <a name="mb-device-services"></a>MB 设备服务


Windows 7 引入了用于支持移动宽带 (MB) 设备的 NDIS （网络设备接口规范） 基于驱动程序模型。 Windows 8 扩展模型来实现基于 USB 的移动宽带设备的标准化的硬件接口。 此硬件接口规范称为作为移动宽带接口模型 (MBIM)。

Windows 8 提供的适用于符合 MBIM 规范的设备的更新后的类驱动程序。 此模型称为 MB 类驱动程序。 但是，任何类驱动程序可以不支持的所有公开的 MB 设备的功能。 若要允许 IHV 合作伙伴以继续进行创新，MB 类驱动程序提供的机制，如[ **IMbnDeviceService 接口**](https://msdn.microsoft.com/library/windows/desktop/hh780509)允许 Ihv 来扩展类驱动程序的行为功能。

**请注意**  通过用户模式应用程序，没有内核模式驱动程序扩展实现功能来扩展 MB 设备服务。

 

虽然类驱动程序中引入 Windows 7 功能有限的 MB 设备功能支持，Windows 8 中的 MB 类驱动程序添加对一些其他功能的本机支持，如 USSD、 SIM/EAP-AKA 和 USB 选择性挂起，并提供可扩展的设备表示形式和控制机制。 [移动宽带的 WinRT API 概述](https://go.microsoft.com/fwlink/p/?linkid=242060)提供一些有关将设备服务扩展的其他信息。

在 Windows 8 MB 类驱动程序，要使用的垂直解决方案提供程序[移动宽带 API 接口](https://msdn.microsoft.com/library/windows/desktop/dd323268)创建之外所提供的 Windows 增强型的用户体验。 扩展机制是一种方法来增加，但不是能替换，请在 MB 类驱动程序本身中受支持的功能。 例如，IHV 可以提供对设备执行固件更新的特定于供应商的软件。 或者，IHV 可以提供特定于供应商提供的软件的增值服务，例如 SIM 工具包 (STK) 或通讯簿。 [AppContainer 移动宽带 pin、 连接和管理](https://go.microsoft.com/fwlink/p/?linkid=320381)示例演示如何在 AppContainer 来访问和管理的移动宽带功能中的 Win32/COM 移动宽带 Api。

除了提供一种机制来扩展 MB 类驱动程序功能，Windows 还提供了机制来启用 Ihv 来部署和安装其软件通过 Windows Update (WU) 增加价值。

有关详细信息，请参阅：

-   "MBIM 服务和 CID 扩展性"部分中的[移动宽带接口模型 (MBIM) 规范]( https://go.microsoft.com/fwlink/p/?linkid=320791)

 

 





