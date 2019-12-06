---
title: 从 WMIS 安装设备元数据包
description: 从 WMIS 安装设备元数据包
ms.assetid: e2466b8a-c9c7-4d0d-9ce7-4648c83fc272
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 487b27b642664b1e0adba7bd8cc3045c3d9cf430
ms.sourcegitcommit: ba3199328ea5d80119eafc399dc989e11e7ae1d6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "74862367"
---
# <a name="installing-device-metadata-packages-from-wmis"></a>从 WMIS 安装设备元数据包


当操作系统检测到新设备时，它会向联机服务查询设备的元数据包的[Windows 元数据和 Internet 服务](windows-metadata-and-internet-services.md)（WMIS）。 如果设备元数据包可用，则在本地计算机上运行的设备元数据检索客户端（DMRC）将从 WMIS 下载包，并将包安装在本地计算机上。

**注意**  如果当前用户是使用只有 guest 权限的任何帐户（如内置的来宾帐户）登录，则不会从 WMIS 下载设备元数据包。

 

如果在将[驱动程序包](driver-packages.md)提交到用于数字签名的[硬件认证包（HCK）](https://go.microsoft.com/fwlink/p/?linkid=227016)时将设备元数据包提交给[Windows 优质 Online Services （Winqual）](https://docs.microsoft.com/windows-hardware/drivers/dashboard/winqual-submission-tool--winqualexe-) ，则在运行 windows 7 和更高版本的 windows 的任何计算机上，您的包将可用于 WMIS 下载请求。

**重要**  强烈建议 oem 仅通过 WMIS 分发设备元数据包。 通过 WMIS 分发设备元数据包支持*硬件第一次*安装方案。 在这种情况下，将安装新的设备，然后安装设备的驱动程序和设备特定软件。 有关此方案的详细信息，请参阅[硬件优先安装](hardware-first-installation.md)。

 

设备元数据包通过 WMIS 通过以下方式安装：

1.  当用户打开 "设备和打印机" 用户界面的 "库" 视图窗口时，[设备元数据检索客户端](device-metadata-retrieval-client.md)（DMRC）将尝试获取设备和打印机用户界面显示的设备的设备元数据。

    DMRC 首先搜索本地计算机的[设备元数据缓存](device-metadata-cache.md)和设备[元数据存储区](device-metadata-store.md)中的设备元数据。 如果设备是新安装的，或者如果设备已计划定期元数据更新，则 DMRC 会在 WMIS 中查询设备的可用元数据包。

2.  如果设备元数据包可用，DMRC 会自动从 WMIS 下载包，提取包的设备元数据组件，并将它们保存在[设备元数据缓存](device-metadata-cache.md)中。

 

 





