---
title: Windows 10 中的 NFC 设备驱动程序
description: 本主题概述了 Windows 10 中 NFC 设备驱动程序的新增功能和改进。
ms.assetid: 07E0E7F4-9D2B-423F-925C-D6923D8D9A4A
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07b842943cacabdd11d28e394d6a0b681cf0173f
ms.sourcegitcommit: 0c3cab853b0b75149b7604eef03275f997792a84
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/26/2020
ms.locfileid: "96157307"
---
# <a name="nfc-device-drivers-in-windows-10"></a>Windows 10 中的 NFC 设备驱动程序

本主题概述了 Windows 10 中 NFC 设备驱动程序的新增功能和改进。

* NFC 设备驱动程序型号已汇聚用于桌面和移动设备，可创建通用 NFC 设备驱动程序模型。 硬件合作伙伴现在可以构建可在所有 Windows 设备平台上运行的单个驱动程序。

* NFC 类扩展 (CX) 实现 Windows 定义的设备驱动程序接口，以便与 NFC 控制器、安全元素和远程 RF 终结点进行交互。

* 添加了内置 NFC 收音机管理器，负责管理 NFC 的飞行模式。 请勿将 IHV 提供的 NFC 无线电管理包与 NFC 驱动程序打包 (在早期版本的 Windows) 中完成。 安装由 IHV 提供的 NFC 无线电管理器和 Windows 10 NFC 收音机管理器将导致这些软件组件之间的冲突。

## <a name="related-topics"></a>相关主题

 [NFC 设备驱动程序接口 (DDI) 参考](/windows-hardware/drivers/ddi/index)  
