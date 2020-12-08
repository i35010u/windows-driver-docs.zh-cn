---
title: 将设备元数据包安装到脱机 Windows 映像
description: 将设备元数据包安装到脱机 Windows 映像
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0536a066c074031100a21d220915e15ac14b7534
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794869"
---
# <a name="installing-device-metadata-packages-to-an-offline-windows-image"></a>将设备元数据包安装到脱机 Windows 映像


计算机 Oem 可以将设备元数据包添加到 Windows 脱机映像，方法是将包复制到本地设备元数据存储。 此存储位于以下位置：

```cpp
%PROGRAMDATA%\Microsoft\Windows\DeviceMetadataStore\<locale>
```

必须首先根据设备元数据包的目标区域设置创建 *&lt; 区域设置 &gt;* 子目录。 然后，必须将该元数据包复制到相应的 *&lt; 区域设置 &gt;* 子目录。

例如，必须将为英国英语本地化的设备元数据包复制到以下位置：

```cpp
%PROGRAMDATA%\Microsoft\Windows\DeviceMetadataStore\EN-GB
```

必须将为日语本地化的设备元数据包复制到以下位置：

```cpp
%PROGRAMDATA%\Microsoft\Windows\DeviceMetadataStore\JA
```

有关详细信息，请参阅 [设备元数据存储](device-metadata-store.md)。

 

 





