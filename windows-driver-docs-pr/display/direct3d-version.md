---
title: DIRECT3D_VERSION
description: DIRECT3D_VERSION
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，头文件
- 标头文件 WDK DirectX 8。0
- DIRECT3D_VERSION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec224b7bf239e20534b9bfb98884de177dd17a3d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809419"
---
# <a name="direct3d_version"></a>DIRECT3D \_ 版本


## <span id="ddk_direct3d_version_gg"></span><span id="DDK_DIRECT3D_VERSION_GG"></span>


DirectX 显示驱动程序必须支持 DirectX 7.0 和更早版本的 DirectX 运行时。 为此，需要同时包含旧的和新的 DirectX 标头，例如 *d3d .h* 和 *d3d8*。 但是，这可能会导致预处理器符号 DIRECT3D 版本的定义出现问题 \_ 。 在标头文件中使用此预处理器符号，以指示应包含哪些结构和函数。 如果尚未 \_ 定义 direct3d 版本，DirectX 标头文件会将 direct3d 版本的值设置 \_ 为其设计所针对的最新版本。 因此， *d3d* 会将 direct3d \_ 版本设置为0x0700，将 *d3d8* 设置为 \_ 0x0800。 如果在 *d3d8* 之前的源中包含 *d3d* ，则不会定义新的 Direct3D 8.0 功能，因此将产生编译器错误。

若要避免此情况，请 \_ 在包含任何标头文件之前，将 DIRECT3D 版本定义为0x0800。 为了获取标头文件中的所有必需符号，请在 *winddi* 或 *d3dnthal* 之前包含 d3d8。

 

 





