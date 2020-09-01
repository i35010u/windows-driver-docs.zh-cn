---
title: 相机微驱动程序示例
description: 相机微驱动程序示例
ms.assetid: a3aa0cf1-9954-4556-8dae-512a12864dfe
ms.date: 05/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: bed0fe5df9ed920aa8bd8d9dcdd87b9f06e6ef5a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187287"
---
# <a name="camera-microdriver-sample"></a>相机微驱动程序示例

[WIA 驱动程序示例](/samples/microsoft/windows-driver-samples/windows-image-acquisition-wia-driver-samples)中的 microdrv 目录包含数字相机的 wia microdriver 示例。

此示例演示如何为相机编写 WIA 用户模式 microdriver。 它通过读取硬盘上某个目录中的图像来模拟照相机。 此示例驱动程序可用作开发的起点，但驱动程序应通过 Windows 提供的一个内核模式驱动程序来访问相机硬件。