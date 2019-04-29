---
title: 打印票证和打印功能提供程序接口
description: 打印机驱动程序实现的打印票证和打印功能提供程序接口
ms.assetid: a14c1173-0419-44c7-bc8f-7197590083b3
keywords:
- 打印机接口 DLL WDK、 打印票证支持
- 打印机接口 DLL WDK，打印功能的支持
- 打印功能 WDK，打印机接口 DLL
- 打印票证 WDK，打印机接口 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac6ea6df77763b73c467ea6e2013663f9cb1ba51
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372081"
---
# <a name="print-ticket-and-print-capabilities-provider-interface-implemented-by-printer-drivers"></a>打印机驱动程序实现的打印票证和打印功能提供程序接口


在 Windows Vista 操作系统的所有驱动程序提供基本的打印票证支持。 但是，支持仅根据信息将公开该驱动程序通过 Microsoft Win32 应用程序编程接口 (Api) 如**DeviceCapabilities**和**GetDeviceCaps**和中的公共部分的设置[ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)结构。 驱动程序可以提供更丰富的体验，通过实现驱动程序的打印票证和打印功能提供程序接口，在以下主题中所述。

打印票证和打印功能提供程序接口的实现必须是多线程安全的因为对提供程序调用驱动应用程序和可能同时进行。

 

 




