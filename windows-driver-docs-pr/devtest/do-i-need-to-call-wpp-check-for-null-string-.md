---
title: 我需要调用 WPP_CHECK_FOR_NULL_STRING
description: 我需要调用 WPP_CHECK_FOR_NULL_STRING
ms.assetid: 4a4dfe91-a70b-4297-9f11-fcc4b0e5a900
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1763ff1609b98b888a0f55d8ab6651282507d77d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341660"
---
# <a name="do-i-need-to-call-wppcheckfornullstring"></a>我需要调用 WPP\_检查\_有关\_NULL\_字符串？


从 Windows 7 版本的 Windows Driver Kit (WDK) 开始，跟踪组件自动检查是否有**NULL**中传递给跟踪函数参数中的字符串。 因此，不需要调用 WPP\_检查\_有关\_NULL\_字符串，以验证每个自变量，以防**NULL**中引发异常的字符串。

如果生成应用[跟踪提供程序](trace-provider.md)（如驱动程序或应用程序） 与 Windows 7 和更高版本的 WDK 中，您可以删除 WPP\_检查\_有关\_NULL\_字符串宏从你的源代码。

 

 





