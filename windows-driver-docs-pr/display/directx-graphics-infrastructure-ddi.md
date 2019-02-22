---
title: DirectX 图形基础结构 DDI
description: DirectX 图形基础结构 DDI
ms.assetid: e4f2bd03-d04b-4f67-94ff-54e023000f35
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0660383fe70fe1ed38af16121eddac78fc8484d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544816"
---
# <a name="directx-graphics-infrastructure-ddi"></a>DirectX 图形基础结构 DDI


DirectX 图形基础结构 (DXGI) 是图形的某些部分更慢发展到开发的。 DXGI 为将来的图形的组件提供一个通用框架。 利用 DXGI 的第一个 Direct3D 运行时版本是 Direct3D 版本 10。 在以前版本的 Direct3D 运行时，Direct3D 运行时中包含对低级别任务的访问。 DXGI 定义从 Direct3D 运行时独立地管理低级别的共享的任务 DDI。 使用 DXGI，现在实现以下任务，并可以使用 DXGI DDI 来处理这些任务：

-   演示文稿

-   伽玛校正控件

-   资源驻留

-   资源优先级

以下部分介绍如何将用户模式显示驱动程序支持和使用 DXGI DDI:

[支持 DXGI DDI](supporting-the-dxgi-ddi.md)

[在资源创建时传递 DXGI 信息](passing-dxgi-information-at-resource-creation-time.md)

[DXGI 演示文稿路径](dxgi-presentation-path.md)

[在注册表中设置 DXGI 信息](setting-dxgi-information-in-the-registry.md)

 

 





