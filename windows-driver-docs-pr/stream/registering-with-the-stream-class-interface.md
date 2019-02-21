---
title: 注册 Stream 类接口
description: 注册 Stream 类接口
ms.assetid: dfc94f8d-0c0a-44ed-a4f8-791ce49aba2d
keywords:
- 视频捕获 WDK AVStream，注册 Stream 类接口
- 捕获视频 WDK AVStream，注册 Stream 类接口
- 注册 Stream 类接口 WDK AVStream
- 正在初始化流数据 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df66766eebcaa06a8d0636c1fd4d9c4c3f9c1c15
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522488"
---
# <a name="registering-with-the-stream-class-interface"></a>注册 Stream 类接口


Stream 类微型驱动程序使用以下步骤来初始化并准备好流式传输数据：

1.  插管理器中检测到微型驱动程序支持的硬件适配器。

2.  插器负责加载微型驱动程序并调用微型驱动程序的[ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程。 中的信息创建一个文件对象**DriverEntry**例程。

3.  微型驱动程序调用 Stream 类接口[ **StreamClassRegisterMinidriver** ](https://msdn.microsoft.com/library/windows/hardware/ff568263)函数从其**DriverEntry**例程，并将传递正确初始化[ **HW\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff559682)结构作为参数。 HW\_初始化\_数据结构包括微型驱动程序函数，用于处理流请求块 (SRB) 命令代码的地址。 这允许微型驱动程序以响应 SRB 代码发送的 Stream 类接口。 中提供了 SRB 命令代码流类支持的完整列表[Stream 类 SRB 引用](https://msdn.microsoft.com/library/windows/hardware/ff568295)。

 

 




