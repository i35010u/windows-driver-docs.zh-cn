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
ms.openlocfilehash: 91197869714680d31935e066ecb4cccb1bd92fce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365803"
---
# <a name="implementing-dynamic-mof-data"></a>实现动态 MOF 数据





通过在运行时的驱动程序的二进制和返回所选的架构信息中包括 MOF 的二进制数据，可以动态发布的驱动程序的架构。 若要提供动态 MOF 数据，驱动程序应执行以下步骤：

1.  编译 MOF 文件中所述[编译的驱动程序的 MOF 文件](compiling-a-driver-s-mof-file.md)。

2.  使用 wmimofck.exe 创建.x 文件将包含创建 MOF 编译器的.bmf 文件的十六进制转储。

3.  使用 **\#包括**包含与驱动程序的源的步骤 2 中创建的十六进制数据。

4.  注册为支持 MSWmi\_MofData\_GUID，它是 wmidata.h 中定义的 GUID。

5.  返回到 WMI 所选的二进制数据，以响应都[ **IRP\_MN\_查询\_所有\_数据**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data)或[ **IRP\_MN\_查询\_单个\_实例**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)请求 MSWmi\_MofData\_GUID。

有关 wmimofck 实用工具的详细信息请参阅[使用 wmimofck.exe](using-wmimofck-exe.md)。

 

 




