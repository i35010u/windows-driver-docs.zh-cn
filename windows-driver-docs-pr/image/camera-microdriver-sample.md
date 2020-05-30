---
title: 相机微驱动程序示例
description: 相机微驱动程序示例
ms.assetid: a3aa0cf1-9954-4556-8dae-512a12864dfe
ms.date: 05/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: 9247a274fc4bf4ca11e232086557dea9589abf3a
ms.sourcegitcommit: 609c5731b2db4c17b9959082c4621c001e012db1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2020
ms.locfileid: "84223531"
---
# <a name="camera-microdriver-sample"></a>相机微驱动程序示例

[WIA 驱动程序示例](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/windows-image-acquisition-wia-driver-samples)中的 microdrv 目录包含数字相机的 wia microdriver 示例。

此示例演示如何为相机编写 WIA 用户模式 microdriver。 它通过读取硬盘上某个目录中的图像来模拟照相机。 此示例驱动程序可用作开发的起点，但驱动程序应通过 Windows 提供的一个内核模式驱动程序来访问相机硬件。
