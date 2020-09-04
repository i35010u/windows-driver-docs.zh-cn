---
ms.assetid: 2274e848-2a0b-445c-82cd-7bcd9e23078a
title: 调试驱动程序
description: 通常，调试内核模式驱动程序需要两台计算机。
ms.date: 08/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7e860bb140d97d4b03743aa91db1227a176f74d4
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065190"
---
# <a name="debugging-a-driver"></a>调试驱动程序

调试内核模式驱动程序需要两台计算机。 调试程序在主计算机  上运行，所调试的代码在目标计算机  上运行。 目标计算机也称为“测试计算机”  。 你可以在主计算机上或在单独的目标计算机上调试用户模式驱动程序。 你必须先为调试配置目标计算机，然后才能够调试目标计算机上运行的驱动程序。

有关调试驱动程序的一般信息，请参阅 [Windows 调试入门](../debugger/getting-started-with-windows-debugging.md)。

有关配置目标计算机和使用网络连接设置调试电缆的信息，请参阅[自动设置 KDNET 网络内核调试](../debugger/setting-up-a-network-debugging-connection-automatically.md)。

## <a name="see-also"></a>另请参阅

[Windows 调试](../debugger/index.md)。