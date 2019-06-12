---
title: 设备元数据存储
description: 设备元数据存储
ms.assetid: 59af6173-28f3-44f5-874e-305bf570d683
keywords:
- 设备元数据存储区 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34758c5bec60d815e183f6165bc18f2e26dd5517
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335266"
---
# <a name="device-metadata-store"></a>设备元数据存储


设备元数据存储是本地计算机存储设备元数据包的目录。 设备元数据存储区访问从下列目录中：

```cpp
%PROGRAMDATA%\Microsoft\Windows\DeviceMetadataStore\<locale>
```

&lt;区域设置&gt;子目录表示设备元数据包的区域设置。 此子目录的名称可以采用以下格式：

```cpp
<Language>[-<Region>] 
```

例如，值为 EN-US 指定包含针对美国英语语言本地化的设备元数据包的子目录。

如果只有 *&lt;语言&gt;* 子目录包含设备元数据的包的指定本地化的语言存在的所有位置中指定的语言。 例如，值为 EN 适用于 EN-US 和 EN-b.

设备元数据包中的以下方法之一复制到设备的元数据存储区：

-   OEM 或开发人员将复制的设备元数据包。 有关详细信息，请参阅[手动添加设备元数据包](manually-adding-device-metadata-packages.md)。

-   使用由 OEM 提供的应用程序进行复制，设备元数据包。 有关详细信息，请参阅[通过应用程序安装设备元数据包](installing-device-metadata-packages-through-an-application.md)。

**请注意**  我们不建议该最终用户复制设备元数据包到设备的元数据存储区。 相反，最终用户应通过使用安装设备元数据包[Windows 元数据和 Internet 服务 (WMIS)](installing-device-metadata-packages-from-wmis.md)或 OEM 提供的应用程序。

 

 

 





