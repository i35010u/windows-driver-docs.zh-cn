---
title: 顺利使用增强式点选打印
description: 更新后的打印机共享机制称为增强点并打印，它允许打印客户端打印到 v4 共享，而无需从打印服务器下载制造商提供的设备驱动程序。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14118a9066f20b1ac71dae5350242d7e83a32987
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831193"
---
# <a name="working-well-with-enhanced-point-and-print"></a>顺利使用增强式点选打印


更新后的打印机共享机制称为增强点并打印，它允许打印客户端打印到 v4 共享，而无需从打印服务器下载制造商提供的设备驱动程序。

因为当客户端计算机与具有增强的点和打印和 v4 打印机驱动程序的打印服务器建立连接时，客户端计算机不会下载整个驱动程序包，因此请务必注意以下体系结构。 此信息可帮助你适当地开发和打包 v4 打印机驱动程序。

## <a name="windows-8-client-connection-behavior"></a>Windows 8 客户端连接行为


当 Windows 8 客户端连接到使用 v4 打印机驱动程序的共享打印队列时，客户端将尝试获取支持客户端呈现的驱动程序。 客户端在本地 DriverStore 中搜索 HardwareID 的驱动程序，该驱动程序与服务器驱动程序的 PrinterDriverID 匹配。 如果找到一个，则将在本地安装该驱动程序。 否则，客户端将使用增强的点和打印驱动程序进行连接。

在这两种情况下，客户端都使用 GetPrinterDataEx 调用从服务器下载配置数据。 配置数据包括一般打印机说明 (GPD) 文件、PostScript 打印机说明 (PPD) 文件、驱动程序属性包、JavaScript 约束和资源 DLL 等数据文件。 客户端还会下载与服务器的驱动程序相关联的 CAT 文件。

然后，打印系统检查客户端，并验证资源 DLL 是否不包含可执行代码。 打印系统还会验证下载的文件是否有效以及是否由从服务器下载的 CAT 文件进行签名。 所有不受信任的文件都将被删除。 下图说明了 Windows 8 客户端与使用 v4 打印机驱动程序的共享打印服务器之间的配置相关通信。

![windows 8 打印客户端与带有 v4 打印驱动程序的打印服务器之间的配置相关通信。 使用 getprinterdataex 调用下载配置信息。](images/win8and-epp.png)

## <a name="windows-7-and-windows-vista-client-connection-behavior"></a>Windows 7 和 Windows Vista 客户端连接行为


Windows 7 和 Windows Vista 客户端还可以连接到使用 v4 打印机驱动程序的共享打印队列。 但在这种情况下，客户端将始终从服务器下载增强的点和打印驱动程序。 此驱动程序使用服务器端呈现来确保为打印机生成正确的打印机描述语言 (PDL) 。

使用 GetPrinterDataEx 调用，通过与 Windows 7 和 Windows Vista 客户端连接相同的方式从服务器下载配置数据。 如果任何下载的文件未通过服务器的 CAT 文件验证，则会将其删除。 下图说明了 Windows 7 或 Windows Vista 客户端与使用 v4 打印机驱动程序的共享打印服务器之间的与配置相关的通信。

![windows 7 或 windows vista 打印客户端与带有 v4 打印驱动程序的打印服务器之间的配置相关通信。 使用 getprinterdataex 调用下载配置信息。](images/win7and-epp.png)

使用 v3 打印机驱动程序支持的共享打印机将继续使用现有的点和打印系统。

## <a name="related-topics"></a>相关主题
[V4 打印机驱动程序开发最佳做法](v4-printer-driver-development-best-practices.md)  



