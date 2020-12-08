---
title: 有关客户端呈现的最佳做法
description: 有关客户端呈现的最佳做法
keywords:
- 客户端渲染 WDK 打印，最佳做法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07b16932bf17b69a30535293b827a038383956ec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797837"
---
# <a name="best-practices-for-client-side-rendering"></a>有关客户端呈现的最佳做法


编写打印机驱动程序时，应考虑以下各项，以使其在客户端呈现时正常工作：

-   打印机驱动程序应安装为驱动程序包。

-   打印机驱动程序应使用 SetPrinterData 或 SetPrinterDataEx 函数存储打印机配置信息。 有关这些函数的详细信息，请参阅 Microsoft Windows SDK 文档。

-   使用自定义打印处理器的打印机驱动程序必须将处理器包含在驱动程序包中，并确保 "指向" 和 "打印" 将其加载到客户端计算机上。

 

 




