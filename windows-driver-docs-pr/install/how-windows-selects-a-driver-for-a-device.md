---
title: Windows 如何为设备选择驱动程序
description: Windows 如何为设备选择驱动程序
ms.assetid: 4c193b97-7b70-425f-99f2-ba976a4cc40a
keywords:
- 驱动程序选择 WDK 设备安装，其中设备设置搜索
ms.date: 03/02/2020
ms.localizationpriority: High
ms.openlocfilehash: e6578fba412ae9b2928fffd53e28e0fc4be09312
ms.sourcegitcommit: c94be6fc464edc94035060a4723efa06ab0f5af9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92153473"
---
# <a name="how-windows-selects-a-driver-for-a-device"></a>Windows 如何为设备选择驱动程序


连接设备时，Windows 需要找到相应的设备驱动程序才能安装。

在 Windows 10 中，此匹配过程分两个阶段进行。 首先，Windows 10 在[驱动程序存储](driver-store.md)中安装最匹配的驱动程序，允许设备快速开始操作。 安装该驱动程序之后，Windows 10 还会：

* 从Windows 更新下载任何匹配的[驱动程序包](driver-packages.md)，并将其放入[驱动程序存储](driver-store.md)。
* 搜索在“设备路径”注册表值指定的位置预加载的驱动程序包  。  “设备路径”注册表值位于以下子项下：`HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion`。  默认情况下，“设备路径”值指定 %SystemRoot%\\INF 目录。

如果 Windows 10 在这些位置找到比初始安装项匹配度更高的驱动程序包，Windows 会将其从驱动程序存储安装的驱动程序替换为匹配度更高的驱动程序。

在 Windows 8 之前的 Windows 版本中，驱动程序匹配进程只在“DevicePath”中查找（如果已指定），否则默认为 Windows 更新  。

下表提供了上述信息的快速摘要：

|搜索阶段|Windows 7 匹配顺序|Windows 8、Windows 10 匹配顺序|
|--- |--- |--- |
|安装驱动程序之前|设备路径；Windows 更新；[驱动程序存储](driver-store.md)|[驱动程序存储](driver-store.md)|
|选择初始驱动程序之后|不适用|**DevicePath** ; Windows Update|


> [!NOTE]
> 在 Windows 10 版本 1709 及更高版本中，Windows 提供了最佳匹配的驱动程序，而这未必是最新的。 驱动程序选择过程考虑硬件 ID、日期/版本和关键/自动/可选类别。 Windows 将关键驱动程序或自动驱动程序的优先级设置为最高。 如果找不到匹配的驱动程序，WU 将查找下一个可选驱动程序。 因此，具有相同值的较旧关键驱动程序优先于较新的可选驱动程序。
> 
> 从 Windows 10 版本 2004 开始，Windows 会搜索计算机和 Windows 更新，仅自动提供最佳的自动/关键匹配驱动程序。 若要查看可选类别中的匹配驱动程序，请转到“设置”>“更新和安全”>“Windows 更新”>“查看可选更新”>“驱动程序更新”。 Windows 仍会使用相同的条件对驱动程序进行排序和选择。
