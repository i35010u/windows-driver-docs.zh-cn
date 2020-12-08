---
title: 发布 WMI 架构
description: 发布 WMI 架构
keywords:
- WMI WDK 内核，发布架构
- 发布 WMI 架构 WDK
- 架构发布 WDK WMI
- MOF 文件 WDK WMI
- 二进制 MOF WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca7b22235161bd121f6f0d6f7401bb1df1008429
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805395"
---
# <a name="publishing-a-wmi-schema"></a>发布 WMI 架构





为了发布 WMI 架构，驱动程序编写器首先会在托管对象格式 (MOF) 语言中创建一个文本文件，该文件包含架构中每个数据块和事件块的类定义，如 [WMI 数据和事件块的 MOF 语法](mof-syntax-for-wmi-data-and-event-blocks.md)中所述。

然后，驱动程序编写器可以通过下列方式之一发布驱动程序的 WMI 架构：

-   编译 MOF 文件，并将其作为资源包含在驱动程序的二进制文件中。 有关详细信息，请参阅 [编译驱动程序的 MOF 文件](compiling-a-driver-s-mof-file.md)。

-   将已编译的 MOF 文件作为资源包含在另一个文件（如 DLL）中，然后将注册表值 **MofImagePath** 添加到该文件的路径，该文件包含在驱动程序的服务密钥下的 MOF。 可以更新以这种方式发布的架构，而无需重新编译该驱动程序。 有关详细信息，请参阅 [设置 MofImagePath 注册表值](setting-the-mofimagepath-registry-value.md)。

-   在驱动程序中包含二进制数据，并在 WMI 请求它时返回。 以这种方式发布的架构可在运行时动态更改。 有关详细信息，请参阅 [实现动态 MOF 数据](implementing-dynamic-mof-data.md)。

 

 




