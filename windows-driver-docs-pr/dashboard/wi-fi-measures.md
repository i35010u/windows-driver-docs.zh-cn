---
title: Wi-Fi 度量
description: Wi-Fi 度量在蓝牙驱动程序外部测试过程中筛选出良性初始化错误
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: bfeb8d94ef2c4be88110128249976960d9e4c99e
ms.sourcegitcommit: 4f08f5686c0bbc27d58930b993cbab1a98e3afb0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89443740"
---
# <a name="wi-fi-measures"></a>Wi-Fi 度量

## <a name="description"></a>说明

Microsoft 通过 WLAN 设备驱动程序接口 (WDI) 提供 WLAN 设备制造商。 与 WDI 兼容的驱动程序使制造商可以开发在设备平台上正常运行的通用驱动程序，提高 WLAN 驱动程序的质量，并降低驱动程序包的复杂性。 计算机可以使用 WDI 兼容的驱动程序，使其 Wi-Fi 组件和 Windows 操作系统可以进行通信并为最终用户启用无线连接。 有关 WDI 驱动程序开发的详细信息，请参阅 [WLAN 通用 Windows 驱动程序模型](../network/wifi-universal-driver-model.md)。

Wi-Fi 度量根据计算机的信号质量筛选出事件，有些会筛选出最差的 5% 的 Wi-fi 连接。 这样可减轻质量评估中的干扰。 
