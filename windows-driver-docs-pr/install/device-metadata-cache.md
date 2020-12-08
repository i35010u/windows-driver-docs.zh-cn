---
title: 设备元数据缓存
description: 设备元数据缓存
keywords:
- 设备元数据缓存 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 858041c6e4d45ac58ddff23e46023967dff0ffb0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827705"
---
# <a name="device-metadata-cache"></a>设备元数据缓存


设备元数据缓存是设备元数据包存储在本地计算机上的目录。

在 Windows 7 上，从以下目录访问设备元数据缓存：

```cpp
%LOCALAPPDATA%\Local\Microsoft\Device Metadata\
```

在 Windows 8 及更高版本中，从以下目录访问设备元数据缓存：

```cpp
%PROGRAMDATA%\Microsoft\Windows\DeviceMetadataCache\
```

当 [设备元数据检索客户端](device-metadata-retrieval-client.md) (DMRC) 从 Windows 元数据和服务 (WMIS) 网站下载设备元数据包时，它会将这些包保存在设备元数据缓存中。 有关此过程的详细信息，请参阅 [从 WMIS 安装设备元数据包](installing-device-metadata-packages-from-wmis.md)。

**注意**   设备元数据缓存只保留给操作系统使用。 不是由 DMRC 安装的设备元数据包，如通过 OEM 提供的应用程序，必须将其复制到 [设备元数据存储](device-metadata-store.md) 。

 

 

 





