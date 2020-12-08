---
title: 平板扫描仪微型驱动程序示例
description: 平板扫描仪微型驱动程序示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea99c1f1b58848fe8a39b3cac2082751980c58ff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808243"
---
# <a name="flatbed-scanner-minidriver-sample"></a>平板扫描仪微型驱动程序示例





Windows DDK 中的 *wiascanr* 目录包含带有文档送纸器的平板扫描仪的示例 WIA 微型驱动程序。

此示例演示如何为扫描仪编写 WIA 用户模式微型驱动程序。 它通过生成测试模式映像来模拟扫描。 此示例驱动程序可用作开发的起点，但驱动程序应通过 Windows 提供的一个内核模式驱动程序来访问扫描程序硬件。 首选的内核模式驱动程序 *usbscan.sys* 和 *scsiscan.sys*。

### <a name="sample-features"></a>示例功能

-   自动文档送纸器功能

    此示例显示了带有自动文档送纸器的平板扫描仪的示例 (ADF) ，以及一个滚动送入扫描器 (无法确定页面长度) 的送纸器。

-   "扫描"、"复制" 和 "传真" 按钮仅支持 (中断事件) 

    运行小型应用程序， *Scanpanl.exe* 随 Windows DDK) 提供 (，以模拟按钮按下。

 

 




