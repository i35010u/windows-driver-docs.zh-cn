---
title: 注册到流类接口
description: 注册到流类接口
ms.assetid: dfc94f8d-0c0a-44ed-a4f8-791ce49aba2d
keywords:
- 视频捕获 WDK AVStream，正在注册 Stream 类接口
- 正在捕获视频 WDK AVStream，正在注册 Stream 类接口
- 注册 Stream 类接口 WDK AVStream
- 初始化流数据 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bb39891ddc1811f8e3da31303b25092cf0cb2aa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843402"
---
# <a name="registering-with-the-stream-class-interface"></a>注册到流类接口


Stream 类微型驱动程序使用以下步骤初始化并准备流式传输数据：

1.  即插即用管理器检测到微型驱动程序支持的硬件适配器。

2.  即插即用管理器加载微型驱动程序并调用微型驱动程序的[*DriverEntry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程。 文件对象是从**DriverEntry**例程中的信息创建的。

3.  微型驱动程序从其**DriverEntry**例程调用 Stream 类接口的[**StreamClassRegisterMinidriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassregisteradapter)函数，并将正确初始化的[**HW\_初始化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)作为参数传递\_数据结构。 \_数据结构的 HW\_初始化包含处理流请求块（SRB）命令代码的微型驱动程序函数的地址。 这允许微型驱动程序响应 Stream 类接口发送的 SRB 代码。 Stream 类支持的 SRB 命令代码的完整列表记录在[Stream 类 SRB 引用](https://docs.microsoft.com/windows-hardware/drivers/stream/stream-class-srb-reference)中。

 

 




