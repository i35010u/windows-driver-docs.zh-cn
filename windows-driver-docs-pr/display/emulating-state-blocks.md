---
title: 模拟状态块
description: 模拟状态块
ms.assetid: 1ede9f1c-f5bb-4f41-8152-63d8663fd99e
keywords:
- 模拟 WDK 显示状态块
- 状态块仿真 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c27b793b62b00370fe7ced6d88c138fa8111d81d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355214"
---
# <a name="emulating-state-blocks"></a>模拟状态块


若要启用 Microsoft Direct3D 运行时，若要模拟状态块，可以按以下方式配置注册表：

```registry
KeyPath   : HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Direct3D
KeyValue  : EmulateStateBlocks
ValueType : REG_DWORD
ValueData : 1 for D3D runtime emulation of stateblocks, 0 for driver implementation (default).
```

**请注意**  配置注册表由 Direct3D 运行时以开启仿真状态块后，运行时不会调用用户模式显示驱动程序[**状态集**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_stateset)函数可设置任何状态块信息。

 

 

 





