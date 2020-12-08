---
title: COM 端口的配置
description: COM 端口的配置
keywords:
- COM 端口 WDK 串行设备
- 串行设备 WDK，COM 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25bc63358d19433d36a4a546494afb3335cbab8f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812069"
---
# <a name="configuration-of-com-ports"></a>COM 端口的配置

从 Windows 2000 开始，COM 端口是一种符合以下附加要求的串行端口：

- 可以通过 COM 端口设备接口类的实例访问 COM 端口。 此类的 GUID 是 \_ \_ 在 Ntddser 中定义的 guid DEVINTERFACE COMPORT。

- 使用在 Ntddser 中定义的 16550 UART 兼容接口操作 COM 端口。

- 若要确保与访问 COM 端口的大多数应用程序的兼容性，应分配使用标准命名约定 "COM <em> &lt; n &gt;</em>" 的符号链接名称，其中 *&lt; n &gt;* 是 com 端口号 (例如，COM1) 。 如果使用 COM <em> &lt; &gt; n</em>名称，则必须从 [com 端口数据库](com-port-database.md)获取 com 端口号 *&lt; n &gt;* 。 COM 端口号只能与 COM<em> &lt; n &gt; </em>名称一起使用。

默认情况下，端口 [设备安装程序类](../install/overview-of-device-setup-classes.md) 和串行函数驱动程序的类安装程序的组合操作将设备配置为 COM 端口。

有关端口类安装程序和串行如何为 COM 端口创建 COM 端口设备接口的信息，请参阅 [com 端口的外部命名](external-naming-of-com-ports.md)。
