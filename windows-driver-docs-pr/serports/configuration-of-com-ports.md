---
title: COM 端口的配置
description: COM 端口的配置
ms.assetid: 519ca9c8-bc67-4a85-87ae-6015c6212dea
keywords:
- COM 端口 WDK 串行设备
- 串行设备 WDK、 COM 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77f94f917f6b9e3606675a560edae0318ceb1ad1
ms.sourcegitcommit: 6a0636c33e28ce2a9a742bae20610f0f3435262c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2019
ms.locfileid: "65836337"
---
# <a name="configuration-of-com-ports"></a>COM 端口的配置

从 Windows 2000 开始，COM 端口是一种串行端口符合以下附加要求：

- 可以通过 COM 端口设备接口类的实例访问的 COM 端口。 此类的 GUID 是 GUID\_DEVINTERFACE\_COMPORT，Ntddser.h 中定义。

- 使用 Ntddser.h 中定义的 16550 UART 兼容接口运行 COM 端口。

- 若要确保兼容的大多数应用程序访问 COM 端口，应分配使用标准命名约定的符号链接名称"COM<em>&lt;n&gt;</em>"，其中 *&lt;n&gt;* 是 COM 端口号 (例如 COM1)。 如果你使用 COM<em>&lt;n&gt;</em> 名称，你必须获取 COM 端口号 *&lt;n&gt;* 从[COM 端口数据库](com-port-database.md). COM 端口号应仅用于 COM<em>&lt;n&gt;</em> 名称。

默认情况下，类安装程序的端口的组合操作[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)和串行函数驱动程序将设备配置为 COM 端口。

端口类安装程序和序列如何创建一个 COM 端口的 COM 端口设备接口的信息，请参阅[外部命名的 COM 端口](external-naming-of-com-ports.md)。
