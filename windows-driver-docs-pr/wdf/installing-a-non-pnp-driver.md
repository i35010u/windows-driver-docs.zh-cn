---
title: 安装非 PnP 驱动程序
description: 安装非 PnP 驱动程序
ms.assetid: 99676d85-feb2-482c-a91b-cfc48be5904c
keywords:
- 内核模式驱动程序框架 WDK，安装驱动程序
- 基于框架的驱动程序 WDK KMDF，安装
- INF 文件 WDK KMDF，非 PnP 驱动程序
- 非 PnP 驱动程序 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2492440c873c6153ec527a635df8270d3b818442
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844775"
---
# <a name="installing-a-non-pnp-driver"></a>安装非 PnP 驱动程序


如果你的驱动程序不支持即插即用（PnP）设备，则驱动程序包必须包含包含 INF <em>DDInstall</em>的 inf 文件 **。CoInstallers**部分和 INF <em>DDInstall</em> **。** [使用 KMDF 共同安装程序](installing-the-framework-s-co-installer.md)中介绍的 WDF 部分。

此外，还必须提供加载驱动程序和框架的共同安装程序的安装程序。 共同安装程序提供了驱动程序的安装程序必须调用的[**WdfPreDeviceInstall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinstaller/nf-wdfinstaller-wdfpredeviceinstall)、 [**WdfPreDeviceInstallEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinstaller/nf-wdfinstaller-wdfpredeviceinstallex)、 [**WdfPostDeviceInstall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinstaller/nf-wdfinstaller-wdfpostdeviceinstall)、 [**WdfPreDeviceRemove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinstaller/nf-wdfinstaller-wdfpredeviceremove)和[**WdfPostDeviceRemove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinstaller/nf-wdfinstaller-wdfpostdeviceremove)函数。

有关如何编写非 PnP 驱动程序的安装程序的示例，请参阅[NONPNP](sample-kmdf-drivers.md)示例附带的安装程序。

 

 





