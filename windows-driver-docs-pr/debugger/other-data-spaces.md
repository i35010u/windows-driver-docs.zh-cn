---
title: 其他数据空间
description: 其他数据空间
ms.assetid: f676a478-c02a-4400-8173-a1b3103c6c1b
keywords:
- 调试器引擎 API、 内存、 数据空间
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 590e163be1ef518f007585244c1952cbf523c9db
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519330"
---
# <a name="other-data-spaces"></a>其他数据空间


## <span id="ddk_other_data_spaces_dbx"></span><span id="DDK_OTHER_DATA_SPACES_DBX"></span>


在内核模式调试中，就可以读取和写入数据到各种数据空间除了主内存和寄存器。 可以访问以下数据空间：

<span id="System_Bus"></span><span id="system_bus"></span><span id="SYSTEM_BUS"></span>系统总线  
方法[ **ReadBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff553519)并[ **WriteBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff561371)读取和写入系统总线数据。

<span id="Control-Space_Memory"></span><span id="control-space_memory"></span><span id="CONTROL-SPACE_MEMORY"></span>Control-Space Memory  
方法[ **ReadControl** ](https://msdn.microsoft.com/library/windows/hardware/ff553524)并[ **WriteControl** ](https://msdn.microsoft.com/library/windows/hardware/ff561374)读取和写入控件空间内存。

<span id="i_o_memory."></span><span id="I_O_MEMORY."></span>I/O： 内存。  
方法[ **ReadIo** ](https://msdn.microsoft.com/library/windows/hardware/ff553573)并[ **WriteIo** ](https://msdn.microsoft.com/library/windows/hardware/ff561402)读取和写入系统和总线 I/O： 内存。

<span id="Model_Specific_Register__MSR_"></span><span id="model_specific_register__msr_"></span><span id="MODEL_SPECIFIC_REGISTER__MSR_"></span>模型特定寄存器 (MSR)  
方法[ **ReadMsr** ](https://msdn.microsoft.com/library/windows/hardware/ff554292)并[ **WriteMsr** ](https://msdn.microsoft.com/library/windows/hardware/ff561424)读取和写入 MSRs，可控制寄存器的启用和禁用功能、 和支持调试，CPU 为特定模型。

### <a name="span-idhandlesspanspan-idhandlesspan-handles"></a><span id="handles"></span><span id="HANDLES"></span> 句柄

在用户模式调试，可以使用系统句柄所拥有的目标进程获取有关系统对象的信息。 该方法[ **ReadHandleData** ](https://msdn.microsoft.com/library/windows/hardware/ff553542)可以用于读取此信息。

可以通过使用获取系统线程和进程的系统对象的句柄[ **GetCurrentThreadHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff545904)并[ **GetCurrentProcessHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff545816)方法。 这些句柄也将提供给[ **IDebugEventCallbacks::CreateThread** ](https://msdn.microsoft.com/library/windows/hardware/ff550713)并[ **IDebugEventCallbacks::CreateProcess** ](https://msdn.microsoft.com/library/windows/hardware/ff550697)创建线程，并创建进程调试事件发生时的回调方法。

**请注意**  在内核模式下，进程和线程句柄是人工句柄。 它们不是系统句柄。

 

 

 





