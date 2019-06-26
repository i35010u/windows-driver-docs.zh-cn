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
ms.openlocfilehash: bc0bcb4b4edf61ff7a2a160d96339ce1afb6ecd3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371139"
---
# <a name="installing-a-non-pnp-driver"></a>安装非 PnP 驱动程序


如果您的驱动程序不支持插即用 (PnP) 设备，驱动程序包必须包含一个 INF 文件，包含 INF <em>DDInstall</em> **。共同安装程序**部分和 INF <em>DDInstall</em> **。WDF**部分中所述[使用 KMDF 共同安装程序](installing-the-framework-s-co-installer.md)。

此外，必须提供加载您的驱动程序和框架的共同安装程序的安装程序。 辅助安装程序提供了[ **WdfPreDeviceInstall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinstaller/nf-wdfinstaller-wdfpredeviceinstall)， [ **WdfPreDeviceInstallEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinstaller/nf-wdfinstaller-wdfpredeviceinstallex)， [ **WdfPostDeviceInstall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinstaller/nf-wdfinstaller-wdfpostdeviceinstall)， [ **WdfPreDeviceRemove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinstaller/nf-wdfinstaller-wdfpredeviceremove)，以及[ **WdfPostDeviceRemove** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinstaller/nf-wdfinstaller-wdfpostdeviceremove)驱动程序的安装程序必须调用的函数。

有关如何为非 PnP 驱动程序编写安装程序的示例，请参阅安装程序附带[NONPNP](sample-kmdf-drivers.md)示例。

 

 





