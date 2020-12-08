---
title: 自定义的 PDEV 结构
description: 自定义的 PDEV 结构
keywords:
- 呈现插件 WDK 打印，PDEV 结构
- PDEV WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5f7214ccbabf9095337c1f0cc424dd77b3d7be5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797385"
---
# <a name="customized-pdev-structures"></a>自定义的 PDEV 结构





呈现插件实现三种方法来支持专用 PDEV 结构。 Unidrv 呈现插件必须实现以下方法：

[**IPrintOemUni::EnablePDEV**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-enablepdev)

[**IPrintOemUni：:D isablePDEV**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-disablepdev)

[**IPrintOemUni::ResetPDEV**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-resetpdev)

Pscript5 呈现插件必须实现以下方法：

[**IPrintOemPS::EnablePDEV**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enablepdev)

[**IPrintOemPS：:D isablePDEV**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-disablepdev)

[**IPrintOemPS::ResetPDEV**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-resetpdev)

PDEV 结构是一个通用术语。 它引用专用的本地定义结构，供定义它的模块使用。 通常，它用于存储物理设备特征。 每个打印机驱动程序和每个呈现插件都定义了其自己的 PDEV 结构。 没有全局定义的类型为 "PDEV" 的结构。

 

