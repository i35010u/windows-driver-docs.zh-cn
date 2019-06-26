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
ms.openlocfilehash: 2542c6bf488fa0d4576c235a5ece19ac1c332ce3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386558"
---
# <a name="dll-start-operations"></a>DLL 启动操作




 

立即加载后 IHV 扩展 DLL，操作系统将调用此序列中的以下 IHV 处理程序函数。

1.  操作系统调用[ *Dot11ExtIhvGetVersionInfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_get_version_info) IHV 处理程序函数来确定支持的 IHV 扩展 DLL 接口版本。 此函数传递一个指向[ **DOT11\_IHV\_版本\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/ns-wlanihv-_dot11_ihv_version_info)结构，后者将该 DLL 的格式设置与最小值和最大接口版本它支持。
    **请注意**  IHV 扩展 DLL 必须设置为 Windows Vista **dwVerMin**并**dwVerMax** DOT11 成员\_IHV\_版本\_为零的信息结构。

     

2.  如果 IHV 扩展 DLL 支持的操作系统支持的接口版本，操作系统将调用[ *Dot11ExtIhvInitService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_service) IHV 处理程序函数以初始化 DLL。

IHV 扩展 DLL 必须遵循这些准则时[ *Dot11ExtIhvInitService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_service)调用。

-   *PDot11ExtAPI*参数包含一个指向[ **DOT11EXT\_API** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/ns-wlanihv-_dot11ext_apis)结构，它使用 IHV 扩展性的地址进行格式设置支持的操作系统的函数。 IHV 扩展 DLL 必须复制 DOT11EXT\_API 结构，它通过引用*pDot11ExtAPI*参数，对全局声明 DOT11EXT\_API 结构。

-   *PDot11IHVHandlers*参数包含一个指向[ **DOT11EXT\_IHV\_处理程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/ns-wlanihv-_dot11ext_ihv_handlers)结构，其中 IHV 扩展 DLL它支持 IHV 处理程序函数的地址的格式。
    **请注意**  DLL 必须未设置的任何成员 DOT11EXT\_IHV\_处理程序结构**NULL**。

     

-   IHV 扩展 DLL 应执行任何内部初始化和资源分配以准备对其 IHV 处理程序函数的调用后返回该 DLL [ *Dot11ExtIhvInitService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_service)。

有关 IHV 扩展性函数的详细信息，请参阅[本机 802.11 IHV 扩展性函数](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-extensibility-functions)。

有关 IHV 处理程序函数的详细信息，请参阅[本机 802.11 IHV 处理程序函数](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-handler-functions)。

 

 





