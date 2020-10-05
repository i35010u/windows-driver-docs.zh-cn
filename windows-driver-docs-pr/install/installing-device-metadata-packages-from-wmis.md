---
title: 从 WMIS 安装设备元数据包
description: 从 WMIS 安装设备元数据包
ms.assetid: e2466b8a-c9c7-4d0d-9ce7-4648c83fc272
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 189bb02f90f7250e23524feb766c5f25e90c099d
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732991"
---
# <a name="installing-device-metadata-packages-from-wmis"></a>从 WMIS 安装设备元数据包


当操作系统检测到新设备时，它会查询一个称为 [Windows 元数据和 Internet 服务](windows-metadata-and-internet-services.md) 的联机服务 (WMIS) 用于设备的元数据包。 如果设备元数据包可用，则在本地计算机上运行的设备元数据检索客户端 (DMRC) 将从 WMIS 下载包，并将包安装在本地计算机上。

**注意**   如果当前用户是使用只有 guest 权限的任何帐户（如内置的来宾帐户）登录，则不会从 WMIS 中下载设备元数据包。

 

如果你将设备元数据包提交给 [Windows 优质 Online Services (Winqual) ](../dashboard/winqual-submission-tool--winqualexe-.md) 在将 [驱动程序包](driver-packages.md) 提交给 [硬件认证工具包 (HCK) ](/previous-versions/windows/hardware/hck/jj124227(v=vs.85)) 进行数字签名时，你的包将可用于在运行 windows 7 和更高版本的 WINDOWS 的任何计算机上的 DMRC 发出的下载请求 WMIS。

**重要提示**   强烈建议 Oem 仅通过 WMIS 分发设备元数据包。 通过 WMIS 分发设备元数据包支持 *硬件第一次* 安装方案。 在这种情况下，将安装新的设备，然后安装设备的驱动程序和设备特定软件。 有关此方案的详细信息，请参阅 [硬件优先安装](hardware-first-installation.md)。

 

设备元数据包通过 WMIS 通过以下方式安装：

1.  当用户打开 "设备和打印机" 用户界面的 "库" 视图窗口时，" [设备元数据检索客户端](device-metadata-retrieval-client.md) (DMRC") 尝试获取设备和打印机用户界面显示的设备的设备元数据。

    DMRC 首先搜索本地计算机的 [设备元数据缓存](device-metadata-cache.md) 和设备 [元数据存储区](device-metadata-store.md) 中的设备元数据。 如果设备是新安装的，或者如果设备已计划定期元数据更新，则 DMRC 会在 WMIS 中查询设备的可用元数据包。

2.  如果设备元数据包可用，DMRC 会自动从 WMIS 下载包，提取包的设备元数据组件，并将它们保存在 [设备元数据缓存](device-metadata-cache.md)中。

