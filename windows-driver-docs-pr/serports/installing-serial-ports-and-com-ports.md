---
title: 安装串行端口和 COM 端口
description: 安装串行端口和 COM 端口
ms.assetid: 9c755dfa-65e5-4ecb-8544-dd63c6b69c8e
keywords:
- WDK 的串行端口
- COM 端口 WDK 串行设备
- 串行驱动程序 WDK、 COM 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00f3d00b7b73fa129886fcaca98a9bace1873ba7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331139"
---
# <a name="installing-serial-ports-and-com-ports"></a>安装串行端口和 COM 端口





适用于大多数设备，端口[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)和串行函数驱动程序提供操作串行端口和 COM 端口所需的功能。 若要安装串行端口和使用这些系统提供的组件的 COM 端口，请执行以下操作：

-   提供与服务的端口指定端口设备安装程序类和串行函数驱动程序的 INF 文件。

-   要将串行端口配置 COM 端口，符合在中定义的要求[配置的 COM 端口](configuration-of-com-ports.md)。

有关安装串行端口和使用的端口设备安装程序类和串行函数驱动程序的 COM 端口的详细信息，请参阅以下主题：

[安装即插串行端口和 COM 端口](installing-plug-and-play-serial-ports-and-com-ports.md)

[安装旧版 COM 端口](installing-legacy-com-ports.md)

如果你执行 COM 端口的自定义安装，您必须遵守中定义的 COM 端口要求[配置的 COM 端口](configuration-of-com-ports.md)。

 

 




