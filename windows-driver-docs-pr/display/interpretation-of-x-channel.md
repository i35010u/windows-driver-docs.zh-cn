---
title: X 通道解释
description: X 通道解释
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示，X 通道
- 扩展格式 WDK Windows 7 显示，X 通道
- X 通道 WDK Windows 7 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db6f3a0001094698c8a40117abfd4bd95a93c17e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792321"
---
# <a name="interpretation-of-x-channel"></a>X 通道解释


本部分仅适用于 Windows 7 及更高版本的操作系统。

用户模式显示驱动程序应以包括 X (的所有格式读取 X 通道例如， \_ \_ \_ 当将此类格式提供给筛选硬件或 BLENDER 时，DXGI 格式 B8G8R8X8 UNORM) 为 1.0 f。

当将数据移出三维管道之外时，必须不修改 X 通道， (即当应用程序调用 **ID3D10Device：： CopyResource**、 **ID3D10Device：： CopySubresourceRegion** 或 **ID3D10Device：： UpdateSubResource** 方法) 时。 有关这些方法的详细信息，请参阅 DirectX SDK 文档。

 

 





