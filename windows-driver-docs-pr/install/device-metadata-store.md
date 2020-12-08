---
title: 设备元数据存储
description: 设备元数据存储
keywords:
- 设备元数据存储 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 046dbab8be3f9d5170c5801dd57474890a5f0eb0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827697"
---
# <a name="device-metadata-store"></a>设备元数据存储


设备元数据存储是设备元数据包存储在本地计算机上的目录。 可从以下目录访问设备元数据存储：

```cpp
%PROGRAMDATA%\Microsoft\Windows\DeviceMetadataStore\<locale>
```

&lt;区域设置 &gt; 子目录表示设备元数据包的区域设置。 此子目录的名称可以是以下格式：

```cpp
<Language>[-<Region>] 
```

例如，如果值为 EN-US，则指定包含设备元数据包的子目录，该程序包已本地化为美国英语语言。

如果只指定了 *&lt; 语言 &gt;* ，则在该语言所在的所有位置都包含为指定语言本地化的设备元数据包的子目录。 例如，"EN" 的值应用于 "EN-US" 和 "EN-US"。

设备元数据包通过以下方式之一复制到设备元数据存储：

-   OEM 或开发人员复制设备元数据包。 有关详细信息，请参阅 [手动添加设备元数据包](manually-adding-device-metadata-packages.md)。

-   使用 OEM 提供的应用程序复制设备元数据包。 有关详细信息，请参阅 [通过应用程序安装设备元数据包](installing-device-metadata-packages-through-an-application.md)。

**注意**   我们不建议最终用户将设备元数据包复制到设备元数据存储。 相反，最终用户应该使用 [Windows 元数据和 Internet 服务 (WMIS) ](installing-device-metadata-packages-from-wmis.md) 或 OEM 提供的应用程序来安装设备元数据包。

 

 

 





