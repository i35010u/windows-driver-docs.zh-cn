---
title: 对 I/O 请求进行 Serenum 筛选
description: 对 I/O 请求进行 Serenum 筛选
ms.assetid: 773688b8-3d5a-48ed-8f20-368cf35fa6e2
keywords:
- Serenum 驱动程序 WDK，I/O 请求筛选
- I/O 请求筛选 WDK Serenum
- 筛选 I/O 请求 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54cb265b18808dd93928bd0d253b785a9eef4562
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387963"
---
# <a name="serenum-filtering-of-io-requests"></a>对 I/O 请求进行 Serenum 筛选





下面介绍 Serenum 筛选器定向到筛选器的 I/O 请求的执行操作：

-   处理与插和电源请求相关联的总线相关操作：
    -   如果存在，删除筛选器执行操作时，请删除 PDO。
    -   枚举响应中的 RS-232 端口[ **IRP\_MN\_查询\_设备\_关系**](https://msdn.microsoft.com/library/windows/hardware/ff551670)类型的请求**BusRelations**.
-   完成 Serenum 特定于设备控制请求返回有关 RS-232 端口的信息。

下面介绍 Serenum 筛选定向到 PDO （PDO 表示附加到 RS-232 端口的子设备） 的 I/O 请求的方式：

-   完成所有插和电源的请求。

-   对筛选器会重新敷设设备控制请求执行操作与 PDO 相关联。

-   完成使 RS-232 端口上的总线关系 Serenum 特定内部设备控制请求。

有关详细信息，请参阅以下文章：

-   [Serenum 驱动程序参考](https://msdn.microsoft.com/library/windows/hardware/ff547040)

-   示例中的代码\\src\\内核\\serenum 目录中 Windows Driver Kit (WDK)

 

 




