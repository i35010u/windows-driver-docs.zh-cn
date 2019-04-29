---
title: 显示驱动程序 DLL 的文件版本格式
description: 本主题介绍用于显示适配器和芯片集显示器驱动程序 Dll 的正确格式设置。
ms.assetid: E39B2A48-D3F8-4EA5-BCF3-23B1053E8D96
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 831415adc7b00cb71eaad09e7bd3fb029577317e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377670"
---
# <a name="file-version-formatting-for-display-driver-dlls"></a>显示驱动程序 DLL 的文件版本格式


本主题介绍了适当的文件格式设置为显示显示适配器或芯片组驱动程序 Dll。

显示的文件版本驱动程序 Dll 必须在窗体 A.BB。抄送。DDDD:

-   一个字段必须设置为 9 以获取 Windows 8 上的 WDDM 1.2 驱动程序。
-   一个字段必须设置为 8 WDDM 1.1 驱动程序在 Windows 7 上。
-   一个字段必须设置为 7 WDDM 1.0 Windows Vista 上的驱动程序。
-   一个字段必须设置为 6 个用于在 Windows Vista 上 XDDM 驱动程序。

对于 Windows 7 和早期版本 (WDDM 1.1 及更早版本) 驱动程序 BB 字段必须设置为该驱动程序支持的 DDI 版本：

-   DirectX 9 的驱动程序 (其中公开任何 D3DDEVCAPS2\_ \* cap) 必须设置为 14 BB。
-   DirectX 10 驱动程序必须设置为 15 BB。
-   Direct3D 11 DDI Direct3D 10 硬件上的驱动程序必须设置为 16 BB。
-   Direct3D 11 DDI 上 Direct3D 11 硬件的驱动程序必须设置为 17 BB。

对于 Windows 8 (WDDM 1.2) 驱动程序 BB 字段必须设置为涵盖的驱动程序的图形硬件上的驱动程序支持的最高 DirectX 功能级别：

-   功能级别 9 驱动程序必须设置为 14 BB。
-   功能级别 10 驱动程序必须设置为 15 BB。
-   功能级别 11 驱动程序必须设置为 17 BB。
-   功能级别 11\_1 驱动程序必须设置为 18 的 BB。

有关 WDDM 1.2 驱动程序，BB 设置以反映功能支持级别，而不考虑硬件 DX 级别，因为 16 是不是特定于 D3D11 DDI DX10 WDDM 1.1 驱动程序的硬件上使用。

抄送字段可为 01 到 9999 之间的任何值相等。

DDDD 字段可以设置为 0 到 9999 之间的任何数字值。

例如：

-   Windows Vista DirectX 9.0 兼容 WDDM 驱动程序可以使用范围 7.14.01.0000 到 7.14.9999.9999。
-   Windows 7 DirectX 10.0 兼容 WDDM 1.1 驱动程序可以使用范围 8.15.01.0000 到 8.15.9999.9999。
-   DX10 硬件上的 Windows 8 WDDM 1.2 驱动程序将 9.15.01.0000 到 9.15.9999.9999。

**建议**（这将成为一项要求的未来版本中）：我们强烈建议的 DriverVer 中显示器驱动程序。INF 文件也符合上述 DLL 版本编号要求，只不过对于 Windows 8，WDDM 1.2 驱动程序 INF DriverVer 中的 BB 字段必须设置为最高上中列出的图形硬件的驱动程序支持的 DirectX 功能级别INF。

 

 





