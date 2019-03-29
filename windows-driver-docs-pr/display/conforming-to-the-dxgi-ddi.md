---
title: 符合 DXGI DDI
description: 符合 DXGI DDI
ms.assetid: 1c789f57-003e-4b29-9a81-dbf194670664
keywords:
- Direct3D 11 版 WDK Windows 7 显示，DXGI DDI 符合性
- Direct3D 11 版 WDK Windows Server 2008 R2 显示，DXGI DDI 符合性
- DirectX 图形基础结构 DDI 符合性 WDK Windows 7 显示
- DirectX 图形基础结构 DDI 符合性 WDK Windows Server 2008 R2 显示
- DXGI DDI 符合性 WDK Windows 7 显示
- DXGI DDI 符合性 WDK Windows Server 2008 R2 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 182fbb7d58a4588850560a912245fa82d7fe799b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576131"
---
# <a name="conforming-to-the-dxgi-ddi"></a>符合 DXGI DDI


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

Direct3D 版本 11 DDI 符合[DirectX 图形基础结构 (DXGI) DDI 的](directx-graphics-infrastructure-ddi.md)资源接口、 设备枚举和演示文稿的定义。

### <a name="span-idpresentationspanspan-idpresentationspanpresentation"></a><span id="presentation"></span><span id="PRESENTATION"></span>演示文稿

Direct3D 11 版的设备必须支持来自任何扫描扩展支持格式的演示文稿，因为用户模式显示驱动程序将要求要向其字段存在操作通过调用颜色转换为其显示微型端口驱动程序 （内核模式驱动程序）从任何其他扫描扩展格式和还为标准 GDI 扫描带格式的扫描扩展格式。 这些扫描扩展格式所知的以下值从 DXGI\_格式枚举：

-   DXGI\_FORMAT\_B5G6R5\_UNORM

-   DXGI\_FORMAT\_B5G5R5A1\_UNORM

-   DXGI\_FORMAT\_B8G8R8A8\_UNORM

-   DXGI\_FORMAT\_B8G8R8X8\_UNORM

使用 Direct3D 版本 11 的后台缓冲区限制 DDI。 如果 DXGI\_使用情况\_后台缓冲区 (从[DXGI\_用法](https://go.microsoft.com/fwlink/p/?linkid=122799)枚举)，则只有其他 DXGI 用法允许如下：

-   DXGI\_使用情况\_SHADERINPUT，映射到 D3D11\_绑定\_着色器\_资源

-   DXGI\_使用情况\_呈现\_目标\_输出，它将映射到 D3D11\_绑定\_呈现\_目标

请注意，无 CPU 访问标志允许的后台缓冲区。

 

 





