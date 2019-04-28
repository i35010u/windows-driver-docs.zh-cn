---
title: 发布 WMI 架构
description: 发布 WMI 架构
ms.assetid: db2b8086-71e4-4532-a0ae-75983691a5a6
keywords:
- WMI WDK 内核，发布架构
- 发布 WMI 架构 WDK
- 发布 WDK WMI 架构
- MOF 文件 WDK WMI
- 二进制 MOF WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8044412f723b88d6aea21518cf950e894a51ab33
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338502"
---
# <a name="publishing-a-wmi-schema"></a>发布 WMI 架构





若要发布 WMI 架构，驱动程序编写器首先创建一个文本文件中包含的类定义的每个数据块和在架构中，事件块的托管对象格式 (MOF) 语言中所述[WMI 数据和事件块MOF语法](mof-syntax-for-wmi-data-and-event-blocks.md).

驱动程序编写器然后可以通过以下方式之一中发布的驱动程序 WMI 架构：

-   编译 MOF 文件并将其包含为驱动程序的二进制映像中的资源。 有关详细信息，请参阅[编译的驱动程序的 MOF 文件](compiling-a-driver-s-mof-file.md)。

-   为不同的文件，如的 DLL 中的资源包括编译的 MOF 文件，添加注册表值**MofImagePath**包含驱动程序的服务密钥下的 MOF 文件的路径。 在这种方式中发布的架构可以无需重新编译该驱动程序更新。 有关详细信息，请参阅[MofImagePath 注册表值设置](setting-the-mofimagepath-registry-value.md)。

-   包括在驱动程序中的二进制数据并将其返回 WMI 请求它时。 在这种方式中发布的架构可以在运行时动态更改。 有关详细信息，请参阅[实现动态 MOF 数据](implementing-dynamic-mof-data.md)。

 

 




