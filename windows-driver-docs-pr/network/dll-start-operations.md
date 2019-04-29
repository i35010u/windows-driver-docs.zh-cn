---
title: DLL 启动操作
description: DLL 启动操作
ms.assetid: cab7a4f9-35dc-44fc-bdd0-30bac8beb652
keywords:
- IHV 扩展 DLL WDK 本机 802.11，开始操作
- 从 IHV 扩展 DLL
- 本机 802.11 IHV 扩展 DLL WDK 启动操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a740d3e94306293d5cfaf5a1f2f682565c2fdce2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379556"
---
# <a name="dll-start-operations"></a>DLL 启动操作




 

立即加载后 IHV 扩展 DLL，操作系统将调用此序列中的以下 IHV 处理程序函数。

1.  操作系统调用[ *Dot11ExtIhvGetVersionInfo* ](https://msdn.microsoft.com/library/windows/hardware/ff547464) IHV 处理程序函数来确定支持的 IHV 扩展 DLL 接口版本。 此函数传递一个指向[ **DOT11\_IHV\_版本\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff548645)结构，后者将该 DLL 的格式设置与最小值和最大接口版本它支持。
    **请注意**  IHV 扩展 DLL 必须设置为 Windows Vista **dwVerMin**并**dwVerMax** DOT11 成员\_IHV\_版本\_为零的信息结构。

     

2.  如果 IHV 扩展 DLL 支持的操作系统支持的接口版本，操作系统将调用[ *Dot11ExtIhvInitService* ](https://msdn.microsoft.com/library/windows/hardware/ff547470) IHV 处理程序函数以初始化 DLL。

IHV 扩展 DLL 必须遵循这些准则时[ *Dot11ExtIhvInitService* ](https://msdn.microsoft.com/library/windows/hardware/ff547470)调用。

-   *PDot11ExtAPI*参数包含一个指向[ **DOT11EXT\_API** ](https://msdn.microsoft.com/library/windows/hardware/ff547617)结构，它使用 IHV 扩展性的地址进行格式设置支持的操作系统的函数。 IHV 扩展 DLL 必须复制 DOT11EXT\_API 结构，它通过引用*pDot11ExtAPI*参数，对全局声明 DOT11EXT\_API 结构。

-   *PDot11IHVHandlers*参数包含一个指向[ **DOT11EXT\_IHV\_处理程序**](https://msdn.microsoft.com/library/windows/hardware/ff547625)结构，其中 IHV 扩展 DLL它支持 IHV 处理程序函数的地址的格式。
    **请注意**  DLL 必须未设置的任何成员 DOT11EXT\_IHV\_处理程序结构**NULL**。

     

-   IHV 扩展 DLL 应执行任何内部初始化和资源分配以准备对其 IHV 处理程序函数的调用后返回该 DLL [ *Dot11ExtIhvInitService*](https://msdn.microsoft.com/library/windows/hardware/ff547470)。

有关 IHV 扩展性函数的详细信息，请参阅[本机 802.11 IHV 扩展性函数](https://msdn.microsoft.com/library/windows/hardware/ff560609)。

有关 IHV 处理程序函数的详细信息，请参阅[本机 802.11 IHV 处理程序函数](https://msdn.microsoft.com/library/windows/hardware/ff560627)。

 

 





