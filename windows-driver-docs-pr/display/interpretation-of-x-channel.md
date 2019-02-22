---
title: X 通道的解释
description: X 通道的解释
ms.assetid: ba039e5a-78ee-43cb-b883-4675b011a29d
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示 X 通道
- 扩展的格式显示 WDK Windows 7 中，X 通道
- 显示 X 通道 WDK Windows 7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be94ebfc01de84d94cdd28a2f24dfd4297753bcb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554058"
---
# <a name="interpretation-of-x-channel"></a>X 通道的解释


本部分仅适用于 Windows 7 和更高版本的操作系统。

用户模式显示驱动程序应读取包含 X 的所有格式中的 X 通道 (例如，DXGI\_格式\_B8G8R8X8\_UNORM) 为 1.0f 时这种格式提供给硬件或 blender 筛选。

X 通道必须复制未修改外部三维管道移动数据时 (即，当应用程序调用**ID3D10Device::CopyResource**， **ID3D10Device::CopySubresourceRegion**，或**ID3D10Device::UpdateSubResource**方法)。 有关这些方法的详细信息，请参阅 DirectX SDK 文档。

 

 





