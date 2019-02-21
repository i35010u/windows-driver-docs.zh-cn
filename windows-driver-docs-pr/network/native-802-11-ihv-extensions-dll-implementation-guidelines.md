---
title: 本机 802.11 IHV 扩展 DLL 实现准则
description: 本机 802.11 IHV 扩展 DLL 实现准则
ms.assetid: ef13de2a-3510-46c5-afb6-0bf1002af5ca
keywords:
- IHV 扩展 DLL WDK 本机 802.11，实施准则
- 本机 802.11 IHV 扩展 DLL WDK，实施准则
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7aa579b3f8af75557259577f65b22d109b14380
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534346"
---
# <a name="native-80211-ihv-extensions-dll-implementation-guidelines"></a>本机 802.11 IHV 扩展 DLL 实现准则




 

IHV 扩展 DLL 作为运行时动态链接库 (DLL) 实现。 有关 Dll 的详细信息，请参阅该主题"有关动态链接库中"在 Microsoft Windows SDK 文档中。

实现 IHV 扩展 DLL 时，请参阅以下准则。

-   Wlanihv.h 中声明的结构和 IHV 扩展 DLL 的引用的函数原型。

-   IHV 扩展 DLL 必须实现[ *Dot11ExtIhvGetVersionInfo* ](https://msdn.microsoft.com/library/windows/hardware/ff547464)并[ *Dot11ExtIhvInitService* ](https://msdn.microsoft.com/library/windows/hardware/ff547470)函数。 此外，这些函数都必须通过使用以生成的 DLL 的模块定义 (.def) 文件导出。 操作系统将通过这些函数的地址解析**GetProcAddress**函数。 有关详细信息**GetProcAddress**，请参阅 Windows SDK 文档。

-   IHV 扩展 DLL 必须实现所有 IHV 处理程序函数。 DLL 对这些函数返回的函数指针的列表，当操作系统将调用[ *Dot11ExtIhvInitService* ](https://msdn.microsoft.com/library/windows/hardware/ff547470)函数。

    有关 IHV 处理程序函数的详细信息，请参阅[本机 802.11 IHV 处理程序函数](https://msdn.microsoft.com/library/windows/hardware/ff560627)。

-   对于 Windows Vista，IHV 扩展 DLL 必须支持接口版本号为零。 当[ *Dot11ExtIhvGetVersionInfo* ](https://msdn.microsoft.com/library/windows/hardware/ff547464)是调用，该 DLL 必须定义所需的最低和最大受支持的界面版本为零。

 

 





