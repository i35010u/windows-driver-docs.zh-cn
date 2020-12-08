---
title: DLL 启动操作
description: DLL 启动操作
keywords:
- IHV 扩展 DLL WDK 本机802.11，启动操作
- 正在启动 IHV 扩展 DLL
- 本机 802.11 IHV 扩展 DLL WDK，启动操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da9fe4546b08c297ad78655d0c8ce1ad65f2433d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788473"
---
# <a name="dll-start-operations"></a>DLL 启动操作




 

加载 IHV 扩展 DLL 后，操作系统会立即按此顺序调用以下 IHV 处理程序函数。

1.  操作系统调用 [*Dot11ExtIhvGetVersionInfo*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_get_version_info) Ihv 处理程序函数来确定 IHV 扩展 DLL 支持的接口版本。 此函数被传递到 [**DOT11 \_ IHV \_ 版本 \_ 信息**](/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11_ihv_version_info) 结构，该结构的 DLL 使用它所支持的最小和最大接口版本进行格式设置。
    **注意**  对于 Windows Vista，IHV 扩展 DLL 必须将 DOT11 IHV 版本信息结构的 **dwVerMin** 和 **dwVerMax** 成员设置 \_ \_ \_ 为零。

     

2.  如果 IHV 扩展 DLL 支持操作系统支持的接口版本，操作系统将调用 [*Dot11ExtIhvInitService*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_service) IHV 处理程序函数来初始化 DLL。

调用 [*Dot11ExtIhvInitService*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_service) 时，必须遵循以下准则。

-   *PDot11ExtAPI* 参数包含指向 [**DOT11EXT \_ api**](/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_apis)结构的指针，该结构的格式为操作系统支持的 IHV 扩展性函数的地址。 IHV 扩展 DLL 必须将 DOT11EXT \_ api 结构（由 *pDot11ExtAPI* 参数引用）复制到全局声明的 DOT11EXT \_ api 结构。

-   *PDot11IHVHandlers* 参数包含指向 [**DOT11EXT \_ ihv \_ 处理程序**](/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_handlers)结构的指针，该结构由 ihv 扩展 DLL 使用它所支持的 IHV 处理程序函数的地址进行格式化。
    **注意**  DLL 不得将 DOT11EXT IHV 处理程序结构的任何成员设置 \_ \_ 为 **NULL**。

     

-   在 DLL 从 [*Dot11ExtIhvInitService*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_service)返回后，IHV 扩展 DLL 应执行任何内部初始化和资源分配，以便为其 IHV 处理程序函数调用做好准备。

有关 IHV 扩展性函数的详细信息，请参阅 [本机 802.11 IHV 扩展性函数](./native-802-11-ihv-extensibility-functions.md)。

有关 IHV 处理程序函数的详细信息，请参阅 [本机 802.11 IHV 处理程序函数](./native-802-11-ihv-handler-functions.md)。

 

 
