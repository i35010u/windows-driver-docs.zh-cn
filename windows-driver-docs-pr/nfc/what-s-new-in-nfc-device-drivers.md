---
title: NFC 设备驱动程序中的新增功能
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
ms.openlocfilehash: 2cd47748d95e912ed0b602d23c39fc77dcea36a3
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382307"
---
# <a name="whats-new-for-nfc-device-drivers-in-windows-10"></a>Windows 10 中的 NFC 设备驱动程序的新增功能


本主题概述了 Windows 10 中 NFC 设备驱动程序的新增功能和改进。

* NFC 设备驱动程序型号已汇聚用于桌面和移动设备，可创建通用 NFC 设备驱动程序模型。 硬件合作伙伴现在可以构建可在所有 Windows 设备平台上运行的单个驱动程序。

* NFC 类扩展 (CX) 实现 Windows 定义的设备驱动程序接口，以便与 NFC 控制器、安全元素和远程 RF 终结点进行交互。

* 添加了内置 NFC 收音机管理器，负责管理 NFC 的飞行模式。 请勿将 IHV 提供的 NFC 无线电管理包与 NFC 驱动程序打包 (在早期版本的 Windows) 中完成。 安装由 IHV 提供的 NFC 无线电管理器和 Windows 10 NFC 收音机管理器将导致这些软件组件之间的冲突。

 
## <a name="related-topics"></a>相关主题
 [NFC 设备驱动程序接口 (DDI) 参考](/windows-hardware/drivers/ddi/index)  
