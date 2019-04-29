---
title: 实现动态 MOF 数据
description: 实现动态 MOF 数据
ms.assetid: 408c0f64-6257-4ece-bb4d-b1850f8ae3c6
keywords:
- WMI WDK 内核，发布架构
- 发布 WMI 架构 WDK
- 发布 WDK WMI 架构
- MOF 文件 WDK WMI
- 动态 MOF 数据 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd436a85f6532977bdda64bad6a7d5411ff9eb30
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365385"
---
# <a name="implementing-dynamic-mof-data"></a>实现动态 MOF 数据





通过在运行时的驱动程序的二进制和返回所选的架构信息中包括 MOF 的二进制数据，可以动态发布的驱动程序的架构。 若要提供动态 MOF 数据，驱动程序应执行以下步骤：

1.  编译 MOF 文件中所述[编译的驱动程序的 MOF 文件](compiling-a-driver-s-mof-file.md)。

2.  使用 wmimofck.exe 创建.x 文件将包含创建 MOF 编译器的.bmf 文件的十六进制转储。

3.  使用**\#包括**包含与驱动程序的源的步骤 2 中创建的十六进制数据。

4.  注册为支持 MSWmi\_MofData\_GUID，它是 wmidata.h 中定义的 GUID。

5.  返回到 WMI 所选的二进制数据，以响应都[ **IRP\_MN\_查询\_所有\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff551650)或[ **IRP\_MN\_查询\_单个\_实例**](https://msdn.microsoft.com/library/windows/hardware/ff551718)请求 MSWmi\_MofData\_GUID。

有关 wmimofck 实用工具的详细信息请参阅[使用 wmimofck.exe](using-wmimofck-exe.md)。

 

 




