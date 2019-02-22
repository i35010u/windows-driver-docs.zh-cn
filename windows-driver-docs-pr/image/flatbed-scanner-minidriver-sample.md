---
title: 平板扫描仪微型驱动程序示例
description: 平板扫描仪微型驱动程序示例
ms.assetid: 8c1ad90a-cff9-45a0-b2d9-e2605436f128
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f87a4e80ceb6be62e781990a80d06286b57a028
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522642"
---
# <a name="flatbed-scanner-minidriver-sample"></a>平板扫描仪微型驱动程序示例





*Wiascanr* Windows DDK 中的目录包含具有文档送纸器平板扫描仪示例 WIA 微型驱动程序。

此示例演示如何编写适用于扫描仪 WIA 用户模式下微型驱动程序。 模拟扫描生成的测试模式映像。 此示例驱动程序可作为起始点进行开发，但您的驱动程序应通过提供与 Windows 的内核模式驱动程序之一访问扫描仪硬件。 首选的内核模式驱动程序*usbscan.sys*并*scsiscan.sys*。

### <a name="sample-features"></a>示例功能

-   自动文档送纸器功能

    此示例演示一个示例，用于与自动文档送纸器 (ADF) 平板扫描仪和滚动馈送扫描程序 （送纸器不能确定页面长度）。

-   扫描、 复制和传真按钮支持 （仅中断事件）

    运行小型应用程序， *Scanpanl.exe* （这提供与 Windows DDK） 来模拟按钮按。

 

 




