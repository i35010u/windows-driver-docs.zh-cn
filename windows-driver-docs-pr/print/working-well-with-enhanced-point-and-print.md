---
title: 还使用增强的指向和打印
description: 为增强的指向和打印，引用更新的打印机共享机制，它允许打印客户端打印到 v4 共享而无需从打印服务器下载制造商提供的设备驱动程序。
ms.assetid: AD01AAD1-B209-419A-B73B-CA746F1B772A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a791b6b9c0c6ae788da290968f6686a27566926d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526429"
---
# <a name="working-well-with-enhanced-point-and-print"></a>还使用增强的指向和打印


为增强的指向和打印，引用更新的打印机共享机制，它允许打印客户端打印到 v4 共享而无需从打印服务器下载制造商提供的设备驱动程序。

因为它们使用已增强，点的打印服务器连接和打印和 v4 打印机驱动程序，它是必须要注意的以下体系结构时，客户端计算机不会下载整个驱动程序包。 此信息应帮助您开发并相应地打包 v4 打印机驱动程序。

## <a name="windows-8-client-connection-behavior"></a>Windows 8 客户端连接行为


当 Windows 8 客户端连接到使用 v4 打印机驱动程序的共享打印队列时，客户端将尝试获取支持客户端呈现的驱动程序。 此客户端搜索匹配服务器驱动程序的 PrinterDriverID 硬件 Id 与本地 DriverStore 驱动程序。 如果找到一个对象，该驱动程序将在本地安装。 否则，客户端将连接使用增强的指向和打印驱动程序。

在这两种情况下，客户端使用 GetPrinterDataEx 调用从服务器下载配置数据。 配置数据包括数据文件，例如通用打印机说明 (GPD) 文件、 PostScript 打印机说明 (PPD) 文件、 驱动程序属性包，JavaScript 约束和资源 DLL。 客户端还会下载已与服务器的驱动程序相关联的 CAT 文件。

然后，打印系统会检查客户端，并验证资源 DLL 包含没有可执行代码。 打印系统还将验证下载的文件有效且经过签名由 CAT 文件从服务器下载。 将删除任何不受信任的文件。 下图说明了此与配置相关的 Windows 8 客户端和共享使用 v4 打印机驱动程序的打印服务器之间通信。

![windows 8 打印客户端和 v4 打印驱动程序的打印服务器之间与配置相关的通信。 使用 getprinterdataex 调用下载配置信息。](images/win8and-epp.png)

## <a name="windows-7-and-windows-vista-client-connection-behavior"></a>Windows 7 和 Windows Vista 客户端连接行为


Windows 7 和 Windows Vista 客户端还可能会连接到使用 v4 打印机驱动程序的共享打印队列。 在这种情况下，但是，客户端将始终增强的指向和打印驱动程序从服务器下载。 此驱动程序使用服务器端呈现，确保打印机生成正确的打印机描述语言 (PDL)。

配置数据是从服务器下载用于 Windows 7 和 Windows Vista 客户端连接，使用 GetPrinterDataEx 调用相同的方式。 如果任何下载的文件未通过验证对服务器的 CAT 文件，它们将被删除。 下图说明了此配置相关 Windows 7 或 Windows Vista 客户端和共享使用 v4 打印机驱动程序的打印服务器之间通信。

![与配置相关的 windows 7 或 windows vista 打印客户端和 v4 打印驱动程序的打印服务器之间通信。 使用 getprinterdataex 调用下载配置信息。](images/win7and-epp.png)

共享的打印机所支持的 v3 打印机驱动程序将继续使用现有的指向和打印系统正常工作。

## <a name="related-topics"></a>相关主题
[V4 打印机驱动程序开发最佳做法](v4-printer-driver-development-best-practices.md)  



