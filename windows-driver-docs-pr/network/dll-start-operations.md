---
title: DLL 启动操作
description: DLL 启动操作
ms.assetid: cab7a4f9-35dc-44fc-bdd0-30bac8beb652
keywords:
- IHV 扩展 DLL WDK 本机802.11，启动操作
- 正在启动 IHV 扩展 DLL
- 本机 802.11 IHV 扩展 DLL WDK，启动操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 873b10569fde25ce9b4bf369532ba5188f04e46c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838134"
---
# <a name="dll-start-operations"></a>DLL 启动操作




 

加载 IHV 扩展 DLL 后，操作系统会立即按此顺序调用以下 IHV 处理程序函数。

1.  操作系统调用[*Dot11ExtIhvGetVersionInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_get_version_info) Ihv 处理程序函数来确定 IHV 扩展 DLL 支持的接口版本。 此函数将被传递到[**DOT11\_IHV\_版本\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11_ihv_version_info)结构，DLL 使用它支持的最小和最大接口版本进行格式设置。
    **注意**  对于 Windows VISTA，IHV 扩展 DLL 必须将 DOT11\_IHV\_\_版本的**dwVerMin**和**dwVerMax**成员设置为零。

     

2.  如果 IHV 扩展 DLL 支持操作系统支持的接口版本，操作系统将调用[*Dot11ExtIhvInitService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_service) IHV 处理程序函数来初始化 DLL。

调用[*Dot11ExtIhvInitService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_service)时，必须遵循以下准则。

-   *PDot11ExtAPI*参数包含指向[**DOT11EXT\_api**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_apis)结构的指针，该结构格式为操作系统支持的 IHV 扩展性函数的地址。 IHV 扩展 DLL 必须将 DOT11EXT\_API 结构（由*pDot11ExtAPI*参数引用）复制到全局声明的 DOT11EXT\_api 结构。

-   *PDot11IHVHandlers*参数包含指向[**DOT11EXT\_IHV\_处理程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_handlers)结构的指针，其中 ihv 扩展 DLL 使用它所支持的 IHV 处理程序函数的地址进行格式化。
    **请注意**  DLL 不得将 DOT11EXT\_IHV\_处理程序结构的任何成员设置为**NULL**。

     

-   在 DLL 从[*Dot11ExtIhvInitService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_service)返回后，IHV 扩展 DLL 应执行任何内部初始化和资源分配，以便为其 IHV 处理程序函数调用做好准备。

有关 IHV 扩展性函数的详细信息，请参阅[本机 802.11 IHV 扩展性函数](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-extensibility-functions)。

有关 IHV 处理程序函数的详细信息，请参阅[本机 802.11 IHV 处理程序函数](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-handler-functions)。

 

 





