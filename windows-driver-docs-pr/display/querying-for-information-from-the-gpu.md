---
title: 从 GPU 查询信息
description: 从 GPU 查询信息
ms.assetid: 0d3942c2-3ae8-4eaa-9780-f146dd49699c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9248a3960b28ca2ba0665cedfd74a8f641ae885
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346230"
---
# <a name="querying-for-information-from-the-gpu"></a>从 GPU 查询信息


Direct3D 运行时可能需要从图形处理单元 (GPU) 的信息，而不输出呈现目标或输出顶点缓冲区。 由于与 CPU 并行执行 GPU，用户模式显示驱动程序应提供高效地公开与 GPU 的通信的异步特性的函数。

查询对象是运行时和驱动程序用于异步通知的资源。 若要创建查询对象，则运行时，首先调用驱动程序的[ **CalcPrivateQuerySize** ](https://msdn.microsoft.com/library/windows/hardware/ff538296)函数，以便该驱动程序可以提供驱动程序需要的查询对象的内存区域的大小。 然后，运行时调用驱动程序的[ **CreateQuery(D3D10)** ](https://msdn.microsoft.com/library/windows/hardware/ff540675)函数来创建查询对象。 在中*CalcPrivateQuerySize*并*CreateQuery(D3D10)* 调用，运行时会提供的查询类型值[ **D3D10DDI\_查询**](https://msdn.microsoft.com/library/windows/hardware/ff541850)中的枚举**查询**的成员[ **D3D10DDIARG\_CREATEQUERY** ](https://msdn.microsoft.com/library/windows/hardware/ff541685)结构*pCreateQuery*参数指向。

每个查询对象实例存在三种状态之一：*构建*，*颁发*，并*发出信号*。 运行时调用的驱动程序[ **QueryBegin** ](https://msdn.microsoft.com/library/windows/hardware/ff569214)函数转换为生成状态的查询对象。

**请注意**  所有查询类型支持*QueryBegin*除外 D3D10DDI\_查询\_事件和 D3D10DDI\_查询\_时间戳。 构建概念不存在 D3D10DDI\_查询\_事件和 D3D10DDI\_查询\_时间戳。

 

运行时调用的驱动程序[ **QueryEnd** ](https://msdn.microsoft.com/library/windows/hardware/ff569217)函数转换为已颁发的状态的查询对象。 以异步方式更高版本的某个时间发生的转换到已发出信号状态。 运行时调用的驱动程序[ **QueryGetData** ](https://msdn.microsoft.com/library/windows/hardware/ff569218)函数来检测该查询是否已转换到已发出信号状态。 如果查询在已发出信号状态下， *QueryGetData*可以传递后将应用于查询的内存区域中的数据的*pData*参数指向。

相同类型的所有查询对象都是先进先出 （即，先入先出）。 例如，所有查询对象的类型 D3D10DDI\_查询\_事件完成按 FIFO 顺序根据其颁发的顺序。 但是，不同类型的查询对象可以完成或发出信号以重叠的顺序。 例如，查询类型 D3D10DDI\_查询\_事件可以完成之前的查询类型 D3D10DDI\_查询\_封闭，即使在运行时发出 D3D10DDI\_查询\_事件查询后，运行时发出 D3D10DDI\_查询\_封闭查询。

当运行时不再需要查询对象时，运行时将释放的内存区域的运行时以前分配给对象和调用的驱动程序[ **DestroyQuery(D3D10)** ](https://msdn.microsoft.com/library/windows/hardware/ff552785)函数通知该驱动程序，该驱动程序将不再能够访问此内存区域。

 

 





