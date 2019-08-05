---
title: 将设备元数据包安装到脱机 Windows 映像
description: 将设备元数据包安装到脱机 Windows 映像
ms.assetid: 53480324-951f-4c51-9b5b-051ce1a3b709
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8fa07b9c066b08e52724f052feec8087c3faf19
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366295"
---
# <a name="installing-device-metadata-packages-to-an-offline-windows-image"></a>将设备元数据包安装到脱机 Windows 映像


计算机 Oem 可以通过将包复制到本地设备元数据存储到脱机 Windows 映像添加设备元数据包。 此存储区是在以下位置：

```cpp
%PROGRAMDATA%\Microsoft\Windows\DeviceMetadataStore\<locale>
```

您必须首先创建 *&lt;区域设置&gt;* 子目录基于设备元数据包的目标区域设置。 然后必须将元数据的包复制到适当 *&lt;区域设置&gt;* 子目录。

例如，设备元数据包的英国英语语言本地化必须复制到以下位置：

```cpp
%PROGRAMDATA%\Microsoft\Windows\DeviceMetadataStore\EN-GB
```

设备元数据包的日语语言本地化必须复制到以下位置：

```cpp
%PROGRAMDATA%\Microsoft\Windows\DeviceMetadataStore\JA
```

有关详细信息，请参阅[设备元数据存储区](device-metadata-store.md)。

 

 





