---
title: 实现动态 MOF 数据
description: 实现动态 MOF 数据
keywords:
- WMI WDK 内核，发布架构
- 发布 WMI 架构 WDK
- 架构发布 WDK WMI
- MOF 文件 WDK WMI
- 动态 MOF 数据 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0f3655f0f517b42ab3f42a249d792c2eedb0959
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788665"
---
# <a name="implementing-dynamic-mof-data"></a>实现动态 MOF 数据





可以通过在驱动程序的二进制文件中包含二进制 MOF 数据并在运行时返回选定的架构信息，来动态发布驱动程序的架构。 若要提供动态 MOF 数据，驱动程序应遵循以下步骤：

1.  编译 MOF 文件，如 [编译驱动程序的 Mof 文件](compiling-a-driver-s-mof-file.md)中所述。

2.  使用 wmimofck.exe 来创建一个文件，该文件将包含 MOF 编译器创建的 bmf 文件的十六进制转储。

3.  使用 " **\# 包括**" 包括在步骤2中使用驱动程序的源创建的十六进制数据。

4.  注册为支持 MSWmi \_ MofData \_ guid，它是在 wmidata 中定义的 guid。

5.  向 WMI 返回所选的二进制数据，以响应 [**IRP \_ MN \_ query \_ ALL \_ data**](./irp-mn-query-all-data.md) Or [**IRP \_ MN \_ query \_ \_**](./irp-mn-query-single-instance.md) requests for MSWmi \_ MofData \_ GUID。

有关 wmimofck 实用工具的详细信息，请参阅 [使用 wmimofck.exe](using-wmimofck-exe.md)。

 

