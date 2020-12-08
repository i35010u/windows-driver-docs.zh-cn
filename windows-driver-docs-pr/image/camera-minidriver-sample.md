---
title: 相机微型驱动程序示例
description: 相机微型驱动程序示例
ms.date: 05/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: 53d6789e61d2f9ba47504879f60bd366940401d3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804155"
---
# <a name="camera-minidriver-sample"></a>相机微型驱动程序示例

[WIA 驱动程序示例](/samples/microsoft/windows-driver-samples/windows-image-acquisition-wia-driver-samples)中的 wiadriverex 目录包含数字相机的 wia 微型驱动程序示例。

此示例演示如何为相机编写 WIA 用户模式微型驱动程序。 它通过读取硬盘上某个目录中的图像来模拟照相机。 此示例驱动程序可用作开发的起点，但驱动程序应通过 Windows 提供的一个内核模式驱动程序来访问相机硬件。
