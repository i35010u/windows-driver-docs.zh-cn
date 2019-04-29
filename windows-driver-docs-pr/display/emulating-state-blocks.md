---
title: 模拟状态块
description: 模拟状态块
ms.assetid: 1ede9f1c-f5bb-4f41-8152-63d8663fd99e
keywords:
- 模拟 WDK 显示状态块
- 状态块仿真 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65f26d3c9d7ee83971f0fa6893b6f5c88c1e49ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355362"
---
# <a name="emulating-state-blocks"></a>模拟状态块


若要启用 Microsoft Direct3D 运行时，若要模拟状态块，可以按以下方式配置注册表：

```registry
KeyPath   : HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Direct3D
KeyValue  : EmulateStateBlocks
ValueType : REG_DWORD
ValueData : 1 for D3D runtime emulation of stateblocks, 0 for driver implementation (default).
```

**请注意**  配置注册表由 Direct3D 运行时以开启仿真状态块后，运行时不会调用用户模式显示驱动程序[**状态集**](https://msdn.microsoft.com/library/windows/hardware/ff569730)函数可设置任何状态块信息。

 

 

 





