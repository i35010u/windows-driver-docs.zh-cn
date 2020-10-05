---
title: Windows 元数据和 Internet 服务
description: Windows 元数据和 Internet 服务
ms.assetid: 9e814be5-e22a-48d5-b46b-d22baa89e229
keywords:
- WMIS
- Metadata Information Server WDK
- 元数据服务器 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7fdb123dd2c7ac918f2801c4c7788421b9cde16
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734267"
---
# <a name="windows-metadata-and-internet-services"></a>Windows 元数据和 Internet 服务


Windows 元数据和 Internet 服务 (WMIS) 管理 Oem 通过 Internet 提交给 [Windows 优质 Online Services (Winqual) ](../dashboard/index.yml) 网站的设备元数据包。 使用 Winqual 站点，可以为 Windows 认证硬件设备和软件应用程序。

当 OEM 提交设备元数据包时，Winqual 完成以下过程：

1.  验证设备元数据包中包含的 XML 文档，并对通过验证的那些包进行数字签名。

2.  使包可用，以便 WMIS 可以在远程计算机上分发和安装。

在 windows 7 和更高版本的 Windows 中，操作系统使用 WMIS 来发现、索引和匹配连接到计算机的特定设备的设备元数据包。 有关此过程的详细信息，请参阅 [从 WMIS 安装设备元数据包](installing-device-metadata-packages-from-wmis.md)。

 

