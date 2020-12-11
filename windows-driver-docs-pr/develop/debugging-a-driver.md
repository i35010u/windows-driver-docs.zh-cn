---
title: 调试驱动程序
description: 通常，调试内核模式驱动程序需要两台计算机。
ms.date: 08/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: 914e51b1da0dc26b049d1566d90ab3e44c6d3191
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787659"
---
# <a name="debugging-a-driver"></a>调试驱动程序

调试内核模式驱动程序需要两台计算机。 调试程序在主计算机  上运行，所调试的代码在目标计算机  上运行。 目标计算机也称为“测试计算机”  。 你可以在主计算机上或在单独的目标计算机上调试用户模式驱动程序。 你必须先为调试配置目标计算机，然后才能够调试目标计算机上运行的驱动程序。

有关调试驱动程序的一般信息，请参阅 [Windows 调试入门](../debugger/getting-started-with-windows-debugging.md)。

有关配置目标计算机和使用网络连接设置调试电缆的信息，请参阅[自动设置 KDNET 网络内核调试](../debugger/setting-up-a-network-debugging-connection-automatically.md)。

## <a name="see-also"></a>另请参阅

[Windows 调试](../debugger/index.md)。
