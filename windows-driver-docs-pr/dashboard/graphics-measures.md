---
title: 显卡度量
description: 显卡度量在显卡驱动程序外部测试过程中筛选出良性初始化错误
ms.topic: article
ms.date: 05/20/2019
ms.author: paslote
author: parkeratmicrosoft
ms.localizationpriority: medium
ms.openlocfilehash: 2aca54633e6ebb4610f0e1d1a8a40cd8708b6f4b
ms.sourcegitcommit: 04da1962e34908adeca54fcf5bbfbaa456efca5f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2019
ms.locfileid: "70223991"
---
# <a name="graphics-measures"></a>显卡度量

[Windows 显示驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/display/roadmap-for-developing-drivers-for-the-windows-vista-display-driver-mo)要求硬件供应商提交配对的用户模式显示驱动程序和内核模式显示驱动程序。 用户模式显示驱动程序在受保护的空间中运行，因此，驱动程序二进制文件中的任何崩溃都不会使计算机崩溃。 相比之下，内核模式驱动程序对计算机功能具有更多的访问权限，并且会在出现错误时使计算机崩溃。 这些驱动程序会一起将操作系统和应用程序中的二进制信息转换为用户可读的视觉对象。 由于显卡和声卡组件会经常交互，因此，还可以通过[音频度量](audio-measures.md)对这些驱动程序进行评估。

此外，一些显卡度量会计算应用程序中用户模式崩溃的次数，并且会计算这些应用程序的使用时间。 然后，这些度量会将使用时间规范化到年，供 Microsoft 用于计算用户在使用该应用程序的一年中将遇到的预期崩溃次数。

显卡驱动程序的适用场景有很多，无法仅在所有外部测试中完全包含这些场景。 因此，某些度量具有“生态系统受众”，以收集更多数据并减少采样噪声，从而提高统计显著性  。 其中一些生态系统度量具有标准受众的度量对等物  。
