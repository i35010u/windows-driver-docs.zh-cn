---
title: 显示驱动程序 DLL 的文件版本格式
description: 本主题介绍适用于显示适配器和芯片组的显示驱动程序 Dll 的正确格式设置。
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 5e3c04311c239b2c9525db09bf1942424a7fc727
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809175"
---
# <a name="file-version-formatting-for-display-driver-dlls"></a>显示驱动程序 DLL 的文件版本格式


本主题介绍了显示适配器或芯片集的显示驱动程序 Dll 的正确文件格式设置。

显示驱动程序 Dll 的文件版本的格式必须为 A.BB。.. DDDD：

-   Windows 8 上的 WDDM 1.2 驱动程序的字段必须设置为9。
-   Windows 7 上的 WDDM 1.1 驱动程序的字段必须设置为8。
-   Windows Vista 上的 WDDM 1.0 驱动程序的字段必须设置为7。
-   Windows Vista 上的 XDDM 驱动程序的字段必须设置为6。

对于 Windows 7 和更早版本 (WDDM 1.1 及更早版本) 驱动程序，必须将 BB 字段设置为驱动程序支持的 DDI 版本：

-    (公开任何 D3DDEVCAPS2 cap) 的 DirectX 9 驱动程序 \_ \* 必须将 BB 设置为14。
-   DirectX 10 驱动程序必须将 BB 设置为15。
-   Direct3D 11-Direct3D 10 硬件上的 DDI 驱动程序必须将 BB 设置为16。
-   Direct3D 11-Direct3D 11 硬件上的 DDI 驱动程序必须将 BB 设置为17。

对于 Windows 8 (WDDM 1.2) 驱动程序必须将 BB 字段设置为驱动程序所涵盖的图形硬件上的驱动程序支持的最高 DirectX 功能级别：

-   功能级别9驱动程序必须将 BB 设置为14。
-   功能级别10驱动程序必须将 BB 设置为15。
-   功能级别11驱动程序必须将 BB 设置为17。
-   功能级别 11 \_ 1 驱动程序必须将 BB 设置为18。

由于对于 WDDM 1.2 驱动程序，BB 设置为反映支持的功能级别，而不考虑硬件 DX 级别，因此不使用16，因为它特定于 WDDM 1.1 驱动程序的 DX10 硬件上的 D3D11 DDI。

"抄送" 字段可以等于01到9999之间的任何值。

可以将 DDDD 字段设置为0到9999之间的任何数字值。

例如：

-   Windows Vista DirectX 9.0 兼容的 WDDM 驱动程序可以使用范围7.14.01.0000 到7.14.9999.9999。
-   Windows 7 DirectX 10.0 兼容的 WDDM 1.1 驱动程序可以使用范围8.15.01.0000 到8.15.9999.9999。
-   DX10 硬件上的 Windows 8 WDDM 1.2 驱动程序将9.15.01.0000 到9.15.9999.9999。

**建议** (在将来的版本) 中，这将成为一项要求：强烈建议在显示驱动程序中 DriverVer。INF 文件还遵循上述 DLL 版本编号要求，但对于 Windows 8、WDDM 1.2 驱动程序，INF DriverVer 中的 BB 字段必须设置为 INF 中列出的图形硬件上驱动程序所支持的最高 DirectX 功能级别。

 

 





