---
title: 模拟状态块
description: 模拟状态块
keywords:
- 模拟状态块 WDK 显示
- 状态块仿真 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca576dd33ff2441f74021c15ec879b54a912c6fd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816883"
---
# <a name="emulating-state-blocks"></a>模拟状态块


若要允许 Microsoft Direct3D 运行时模拟状态块，可以按以下方式配置注册表：

```registry
KeyPath   : HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Direct3D
KeyValue  : EmulateStateBlocks
ValueType : REG_DWORD
ValueData : 1 for D3D runtime emulation of stateblocks, 0 for driver implementation (default).
```

**注意**   将注册表配置为启用 Direct3D 运行时对状态块的模拟后，运行时不会调用用户模式显示驱动程序的 [**StateSet**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_stateset) 函数来设置任何状态块信息。

 

 

