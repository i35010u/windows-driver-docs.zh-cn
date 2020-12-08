---
title: 安装即插即用串行端口和 COM 端口
description: 安装即插即用串行端口和 COM 端口
keywords:
- 串行驱动程序 WDK，即插即用设备
- 即插即用串行设备 WDK
- 串行设备 WDK，即插即用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d689ad66718c7a0d5c7686f331d14aa7ebb5f1ef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812015"
---
# <a name="installing-plug-and-play-serial-ports-and-com-ports"></a>安装即插即用串行端口和 COM 端口





默认情况下，端口类安装程序和串行函数驱动程序的组合操作将串行端口配置为 COM 端口。 如果设备的 **SerialSkipExternalNaming** 条目值不存在或设置为零，则串行端口将为串行端口创建 COM 端口设备接口。 有关串行如何为 COM 端口创建 COM 端口设备接口以及如何覆盖此操作的详细信息，请参阅 [Com 端口的外部命名](external-naming-of-com-ports.md)。

端口类安装程序会在安装串行端口时执行以下任务：

1. 选择一个 COM 端口号，并在设备硬件密钥下的 **portvalue** 条目值中设置端口名称。 端口名称的格式为 COM <em> &lt; n &gt;</em>，其中 *&lt; n &gt;* 为端口号。 如果串行端口为串行端口创建了一个 COM 端口接口，则串行使用 **portvalue** 的值作为 COM 端口的符号链接名称。

2. 显示 "默认属性页" 对话框，该对话框允许用户选择端口设置。 有关如何安装自定义属性页的信息，请参阅 [安装 COM 端口的高级属性页](installing-an-advanced-properties-page-for-a-com-port.md)。

3. 设置设备的设备友好名称。 使用 \_ **SETUPDIGETDEVICEREGISTRYPROPERTY** 的 SPDRP FRIENDLYNAME 标志获取名称。

可以提供共同安装程序，为 [即插即用串行设备设置注册表设置](registry-settings-for-a-plug-and-play-serial-device.md)。 如果注册表中不存在条目值，则串行将使用端口的默认值。

 

 




