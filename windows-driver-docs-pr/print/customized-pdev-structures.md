---
title: 自定义的 PDEV 结构
description: 自定义的 PDEV 结构
ms.assetid: e5c51b9a-5f73-4411-88d8-931981a8450c
keywords:
- 呈现 WDK 打印，PDEV 结构的插件
- PDEV WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 819287a94b9decbd918cbf1dd7d857e850ac2269
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525128"
---
# <a name="customized-pdev-structures"></a>自定义的 PDEV 结构





呈现插件实现三个方法，以支持专用 PDEV 结构。 Unidrv 呈现插件必须实现以下方法：

[**IPrintOemUni::EnablePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff554249)

[**IPrintOemUni::DisablePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff554238)

[**IPrintOemUni::ResetPDEV**](https://msdn.microsoft.com/library/windows/hardware/ff554270)

Pscript5 呈现插件必须实现以下方法：

[**IPrintOemPS::EnablePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff553215)

[**IPrintOemPS::DisablePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff553209)

[**IPrintOemPS::ResetPDEV**](https://msdn.microsoft.com/library/windows/hardware/ff553233)

PDEV 结构是一个通用的词条。 它表示一个专用的本地定义的结构，用于使用通过定义它的模块。 通常情况下，它用于存储物理设备特性。 每个打印机驱动程序和每个呈现的插件，定义其自己 PDEV 结构。 没有任何全局定义的类型"PDEV"结构。

 

 




