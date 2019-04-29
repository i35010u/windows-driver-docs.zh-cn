---
title: 从 WMIS 安装设备元数据包
description: 从 WMIS 安装设备元数据包
ms.assetid: e2466b8a-c9c7-4d0d-9ce7-4648c83fc272
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bb0f72b149433dfa980fa4d0135dae4e09b28d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387219"
---
# <a name="installing-device-metadata-packages-from-wmis"></a>从 WMIS 安装设备元数据包


当操作系统检测到新设备时，它会查询名为的联机服务[Windows 元数据和 Internet 服务](windows-metadata-and-internet-services.md)(WMIS) 的设备元数据包。 如果可用的设备元数据包，设备元数据检索客户端 （dmrc 如何），在本地计算机上运行从 WMIS 下载包，并在本地计算机上安装包。

**请注意**  如果当前用户的任何帐户使用仅来宾特权，例如内置的来宾帐户登录，从 WMIS 不下载设备元数据包。

 

如果提交到您设备元数据包[Windows Quality Online Services (Winqual)](https://go.microsoft.com/fwlink/p/?linkid=62651)提交时您[驱动程序包](driver-packages.md)到[硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?linkid=227016)进行数字签名，你的包将可供 WMIS 发出的 dmrc 如何运行 Windows 7 和更高版本 Windows 的任何计算机上的下载请求。

**重要**  我们强烈建议 Oem 分发只能通过 WMIS 设备元数据包。 设备元数据的分发包 WMIS 支持通过*硬件优先*安装方案。 在此方案中，该驱动程序之前安装了新设备和设备的特定于设备的软件安装。 有关此方案的详细信息，请参阅[硬件第一个安装](hardware-first-installation.md)。

 

设备元数据包通过 WMIS 安装如下所示：

1.  在用户打开设备和打印机用户界面，在库视图窗口时[设备元数据检索客户端](device-metadata-retrieval-client.md)(DMRC) 尝试获取的设备的设备元数据的设备和打印机用户界面显示。

    Dmrc 如何首先搜索本地计算机[设备元数据缓存](device-metadata-cache.md)并[设备元数据存储区](device-metadata-store.md)为设备元数据。 如果新安装该设备，或者设备已计划定期的元数据更新，dmrc 如何查询设备的可用元数据包 WMIS。

2.  如果可用的设备元数据包，dmrc 如何自动从 WMIS 下载包、 提取包的设备元数据组件，并将存储在[设备元数据缓存](device-metadata-cache.md)。

 

 





