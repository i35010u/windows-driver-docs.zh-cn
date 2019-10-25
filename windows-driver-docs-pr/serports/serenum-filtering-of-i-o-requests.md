---
title: 对 I/O 请求进行 Serenum 筛选
description: 对 I/O 请求进行 Serenum 筛选
ms.assetid: 773688b8-3d5a-48ed-8f20-368cf35fa6e2
keywords:
- Serenum driver WDK，i/o 请求筛选
- I/o 请求筛选 WDK Serenum
- 筛选 i/o 请求 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bdcce5256b7ac05fe328a3e6c4b6beb9eb4db56
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845396"
---
# <a name="serenum-filtering-of-io-requests"></a>对 I/O 请求进行 Serenum 筛选

下面介绍 Serenum 如何筛选定向到筛选器的 i/o 请求：

- 处理与即插即用和电源请求关联的与总线相关的操作：
    -   删除筛选器时，删除 PDO （如果存在）。
    -   枚举 RS-232 端口以响应[**IRP\_MN\_QUERY\_设备\_关系**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)请求类型为**BusRelations**。
- 完成返回 Serenum 端口232相关信息的特定于设备的设备控制请求。

下面介绍了 Serenum 如何筛选定向到 PDO 的 i/o 请求（PDO 表示连接到 RS-232 端口的子设备）：

- 完成所有即插即用和电源请求。

- 将设备控制请求重置为与 PDO 关联的筛选器。

- 完成一个 Serenum 特定的内部设备控制请求，该请求使 RS-232 端口上的总线关系无效。

有关详细信息，请参阅以下内容：

- [ntddser 标头](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/)

- Windows 驱动程序工具包（WDK）中 \\src\\内核\\serenum 目录的示例代码
