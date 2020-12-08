---
title: DirectX 图形基础结构 DDI
description: DirectX 图形基础结构 DDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 461651fa481a7b91527adbbbf9783ac4812697b6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809339"
---
# <a name="directx-graphics-infrastructure-ddi"></a>DirectX 图形基础结构 DDI


DirectX 图形基础结构 (DXGI) 是通过实现实现的，因为图形的某些部分的发展速度比其他部分更慢。 DXGI 为未来图形组件提供了通用框架。 使用 DXGI 的第一个 Direct3D 运行时版本是 Direct3D 版本10。 在以前版本的 Direct3D 运行时中，对低级别任务的访问包含在 Direct3D 运行时中。 DXGI 定义独立于 Direct3D 运行时管理低级别共享任务的 DDI。 以下任务现在使用 DXGI 实现，你可以使用 DXGI DDI 来处理这些任务：

-   呈现

-   伽玛更正控件

-   资源驻留

-   资源优先级

以下部分介绍用户模式显示驱动程序如何支持和使用 DXGI DDI：

[支持 DXGI DDI](supporting-the-dxgi-ddi.md)

[创建资源时传递 DXGI 信息](passing-dxgi-information-at-resource-creation-time.md)

[DXGI 呈现路径](dxgi-presentation-path.md)

[在注册表中设置 DXGI 信息](setting-dxgi-information-in-the-registry.md)

 

 





