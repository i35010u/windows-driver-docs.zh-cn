---
title: 打印驱动程序中的打印票证处理
description: 打印驱动程序中的打印票证处理
ms.assetid: a7295632-0133-4133-b62e-5526dcc12c7d
keywords:
- 打印票证 WDK、 打印驱动程序处理
- 打印票证 WDK，XPSDrv
- 打印票证 WDK，基于 GDI 的打印驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bb37596b19b3f473a3d5159d40a797770017748
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351859"
---
# <a name="print-ticket-processing-in-the-print-driver"></a>打印驱动程序中的打印票证处理


PrintTicket 对象中的验证的设置用于配置打印 XPSDrv 打印机驱动程序执行的处理。 组件的打印驱动程序，因此，必须阅读并解释驱动程序执行任何处理，因此驱动程序可以处理这些设置根据文档前打印票证中的设置。

XPSDrv 打印驱动程序的打印驱动程序的打印处理筛选器中执行此处理。

基于 GDI 的打印驱动程序继续使用[ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)结构由于 Windows Vista 中内置了兼容性支持的设置打印子系统。 有关这种支持的详细信息，请参阅[Win 32 应用程序的打印票证兼容性](print-ticket-compatibility-with-win-32-applications.md)。

有关实现打印机驱动程序中处理的打印票证的详细信息，请参阅[XPSDrv 呈现模块中的打印票证支持](print-ticket-support-in-the-xpsdrv-render-module.md)。

 

 




