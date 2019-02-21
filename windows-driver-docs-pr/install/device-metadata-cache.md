---
title: 设备元数据缓存
description: 设备元数据缓存
ms.assetid: 0b20e1e0-9137-4572-8a5b-6bde63c34ce4
keywords:
- 设备元数据缓存 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25d7d9324654be1033323127a6ba145bb9ca4c12
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519365"
---
# <a name="device-metadata-cache"></a>设备元数据缓存


设备元数据缓存是在本地计算机存储设备元数据包的目录。

在 Windows 7 设备元数据缓存访问从以下目录：

```cpp
%LOCALAPPDATA%\Local\Microsoft\Device Metadata\
```

Windows 8 及更高版本，从下列目录访问设备元数据缓存：

```cpp
%PROGRAMDATA%\Microsoft\Windows\DeviceMetadataCache\
```

当[设备元数据检索客户端](device-metadata-retrieval-client.md)(DMRC) 从 Windows 元数据和服务 (WMIS) 网站下载设备元数据包，它将它们保存在设备元数据缓存。 有关此过程的详细信息，请参阅[WMIS 从安装设备元数据包](installing-device-metadata-packages-from-wmis.md)。

**请注意**  设备元数据缓存保留为仅操作系统使用。 设备元数据包的情况下不安装 dmrc 如何，例如通过提供的 OEM，应用程序必须复制到[设备元数据存储区](device-metadata-store.md)相反。

 

 

 





