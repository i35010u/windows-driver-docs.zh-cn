---
title: 自定义的 PDEV 结构
description: 自定义的 PDEV 结构
ms.assetid: e5c51b9a-5f73-4411-88d8-931981a8450c
keywords:
- 呈现插件 WDK 打印，PDEV 结构
- PDEV WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31332cae91089f48b061749173a2bbe7f2dc6d4d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218246"
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

 

