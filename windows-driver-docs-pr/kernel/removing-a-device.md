---
title: 删除设备
description: 删除设备
ms.assetid: 8184987f-5c46-4dd6-aad2-3c32b14205fd
keywords:
- 即插即用 WDK 内核，删除设备
- 即插即用和播放 WDK 内核，删除设备
- 删除设备
- 通知 WDK 即插即用，删除设备
- WDK PnP Irp
- I/O 请求数据包 WDK 即插即用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2033825edfa1e8b00f056f58fe6bd45c5227cfbb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542352"
---
# <a name="removing-a-device"></a>删除设备





PnP 管理器指示驱动程序的设备，或正在从计算机中以物理方式删除时删除设备及其设备对象。 PnP 管理器还会发送*删除*IRP，当用户请求更新的驱动程序的设备以及在 Windows 2000 及更高版本，设备被禁用，或无法启动时。

以下部分介绍当 PnP 管理器发出*删除*Irp 和驱动程序应如何响应这些 Irp。 本部分介绍以下主题：

[了解何时删除 Irp 颁发](understanding-when-remove-irps-are-issued.md)

[处理 IRP\_MN\_查询\_删除\_设备请求](handling-an-irp-mn-query-remove-device-request.md)

[处理 IRP\_MN\_删除\_设备请求](handling-an-irp-mn-remove-device-request.md)

[处理 IRP\_MN\_取消\_删除\_设备请求](handling-an-irp-mn-cancel-remove-device-request.md)

[处理 IRP\_MN\_惊讶\_删除请求](handling-an-irp-mn-surprise-removal-request.md)

[使用删除锁定](using-remove-locks.md)

 

 




