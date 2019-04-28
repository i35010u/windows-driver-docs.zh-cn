---
title: Windows 元数据和 Internet 服务
description: Windows 元数据和 Internet 服务
ms.assetid: 9e814be5-e22a-48d5-b46b-d22baa89e229
keywords:
- WMIS
- 元数据信息 Server WDK
- 元数据服务器 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e69ca81bdec134728d3dbd31b634ae3cbfb08ffa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339261"
---
# <a name="windows-metadata-and-internet-services"></a>Windows 元数据和 Internet 服务


Windows 元数据和 Internet 服务 (WMIS) 管理 Oem 将提交到的设备元数据包[Windows Quality Online Services (Winqual)](https://go.microsoft.com/fwlink/p/?linkid=62651)通过 Internet 的网站。 通过使用 Winqual 站点，你可以认证硬件设备和 Windows 的软件应用程序。

当 OEM 提交设备元数据包时，Winqual 将完成以下过程：

1.  验证设备元数据包中, 包含的 XML 文档和数字签名通过验证这些包。

2.  使包可用，以便 WMIS 可以分发和安装在远程计算机上。

在 Windows 7 和更高版本的 Windows 中，操作系统使用 WMIS 发现索引，并将匹配连接到计算机的特定设备的设备元数据包。 有关此过程的详细信息，请参阅[WMIS 从安装设备元数据包](installing-device-metadata-packages-from-wmis.md)。

 

 





