---
title: 模拟状态块
description: 模拟状态块
ms.assetid: 1ede9f1c-f5bb-4f41-8152-63d8663fd99e
keywords:
- 模拟状态块 WDK 显示
- 状态块仿真 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1dfcd3252c13f26298dd7a9b0bcd0ef8f93c0569
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839708"
---
# <a name="emulating-state-blocks"></a>模拟状态块


若要允许 Microsoft Direct3D 运行时模拟状态块，可以按以下方式配置注册表：

```registry
KeyPath   : HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Direct3D
KeyValue  : EmulateStateBlocks
ValueType : REG_DWORD
ValueData : 1 for D3D runtime emulation of stateblocks, 0 for driver implementation (default).
```

**请注意**   将注册表配置为启用 Direct3D 运行时对状态块的仿真后，运行时不会调用用户模式显示驱动程序的[**StateSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_stateset)函数来设置任何状态块信息。

 

 

 





