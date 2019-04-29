---
title: 输出合并器阶段
description: 输出合并器阶段
ms.assetid: 9b549614-0f51-4c79-a6c4-ba907a5f9068
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3de6b397b57ae785c386d2aabc7c5a023ad44df8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358349"
---
# <a name="output-merger-stage"></a>输出合并器阶段


逻辑管道的最后一步是可见性决定，通过模具或深度，并编写或值混合处理的输出呈现器目标，可以是多个资源类型之一。 在输出混合阶段定义这些操作，以及输出资源 （呈现器目标） 的绑定。

Direct3D 运行时调用以下的驱动程序函数，来创建、 设置、 清除和销毁输出：

[**CalcPrivateBlendStateSize**](https://msdn.microsoft.com/library/windows/hardware/ff538274)

[**CalcPrivateDepthStencilStateSize**](https://msdn.microsoft.com/library/windows/hardware/ff538282)

[**CalcPrivateDepthStencilViewSize**](https://msdn.microsoft.com/library/windows/hardware/ff538284)

[**ClearDepthStencilView**](https://msdn.microsoft.com/library/windows/hardware/ff539408)

[**ClearRenderTargetView**](https://msdn.microsoft.com/library/windows/hardware/ff539409)

[**CreateBlendState**](https://msdn.microsoft.com/library/windows/hardware/ff540594)

[**CreateDepthStencilState**](https://msdn.microsoft.com/library/windows/hardware/ff540627)

[**CreateDepthStencilView**](https://msdn.microsoft.com/library/windows/hardware/ff540629)

[**DestroyBlendState**](https://msdn.microsoft.com/library/windows/hardware/ff552745)

[**DestroyDepthStencilState**](https://msdn.microsoft.com/library/windows/hardware/ff552759)

[**DestroyDepthStencilView**](https://msdn.microsoft.com/library/windows/hardware/ff552762)

[**SetBlendState**](https://msdn.microsoft.com/library/windows/hardware/ff569527)

[**SetDepthStencilState**](https://msdn.microsoft.com/library/windows/hardware/ff569532)

[**SetPredication**](https://msdn.microsoft.com/library/windows/hardware/ff569547)

[**SetRenderTargets**](https://msdn.microsoft.com/library/windows/hardware/ff569553)

[**SetTextFilterSize**](https://msdn.microsoft.com/library/windows/hardware/ff569663)

 

 





