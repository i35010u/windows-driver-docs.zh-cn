---
title: 相机微型驱动程序示例
description: 相机微型驱动程序示例
ms.assetid: 82ed48e9-2e3e-4386-bb89-03e3c5ff92b0
ms.date: 05/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: f593911d1314f10b3fcede1f82b7136cc207e556
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193253"
---
# <a name="camera-minidriver-sample"></a>相机微型驱动程序示例

[WIA 驱动程序示例](/samples/microsoft/windows-driver-samples/windows-image-acquisition-wia-driver-samples)中的 wiadriverex 目录包含数字相机的 wia 微型驱动程序示例。

此示例演示如何为相机编写 WIA 用户模式微型驱动程序。 它通过读取硬盘上某个目录中的图像来模拟照相机。 此示例驱动程序可用作开发的起点，但驱动程序应通过 Windows 提供的一个内核模式驱动程序来访问相机硬件。