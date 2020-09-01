---
title: 使用 Windows 调试器调试 Windows 应用程序
description: 可以使用 Windows 调试器 (WinDbg、CDB 和 NTSD) 调试 Windows 应用。 在调试时，可以使用 PLMDebug 工具控制挂起、继续和终止 Windows 应用程序。
ms.assetid: 87AA23A1-AB70-48CC-8F96-350C121F250E
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 543dd85a6da85e92cc86ed2be04be4ce8d5516c9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216733"
---
# <a name="debugging-windows-apps-using-the-windows-debugger"></a>使用 Windows 调试器调试 Windows 应用程序


可以使用 Windows 调试器 (WinDbg、CDB 和 NTSD) 调试 Windows 应用。 在调试时，可以使用 [**PLMDebug**](plmdebug.md) 工具控制挂起、继续和终止 Windows 应用程序。

若要调试托管代码 Windows 应用，请加载 [SOS 调试扩展 ( # A0) ](/dotnet/framework/tools/sos-dll-sos-debugging-extension) 和 ( # A1) 的数据访问组件。 有关详细信息，请参阅 [使用 Windows 调试器调试托管代码](debugging-managed-code.md)。

Windows 调试器独立于 Visual Studio 调试器。 有关 windows 调试器和 Visual Studio 调试器之间的区别的信息，请参阅 [Windows 调试](index.md)。

 

