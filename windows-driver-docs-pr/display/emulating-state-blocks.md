---
title: 模拟状态块
description: 模拟状态块
ms.assetid: 1ede9f1c-f5bb-4f41-8152-63d8663fd99e
keywords:
- 模拟状态块 WDK 显示
- 状态块仿真 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9be00b289ff7465d6880e37e3f2c118e93bfe8f8
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065874"
---
# <a name="emulating-state-blocks"></a>模拟状态块


若要允许 Microsoft Direct3D 运行时模拟状态块，可以按以下方式配置注册表：

```registry
KeyPath   : HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Direct3D
KeyValue  : EmulateStateBlocks
ValueType : REG_DWORD
ValueData : 1 for D3D runtime emulation of stateblocks, 0 for driver implementation (default).
```

**注意**   将注册表配置为启用 Direct3D 运行时对状态块的模拟后，运行时不会调用用户模式显示驱动程序的[**StateSet**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_stateset)函数来设置任何状态块信息。

 

 

