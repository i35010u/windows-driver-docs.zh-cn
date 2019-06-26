---
title: 本机 802.11 IHV 扩展 DLL 实现指导原则
description: 本机 802.11 IHV 扩展 DLL 实现指导原则
ms.assetid: ef13de2a-3510-46c5-afb6-0bf1002af5ca
keywords:
- IHV 扩展 DLL WDK 本机 802.11，实施准则
- 本机 802.11 IHV 扩展 DLL WDK，实施准则
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3e08f32e283e76e5d011843416216485cca470c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387288"
---
# <a name="native-80211-ihv-extensions-dll-implementation-guidelines"></a>本机 802.11 IHV 扩展 DLL 实现指导原则




 

IHV 扩展 DLL 作为运行时动态链接库 (DLL) 实现。 有关 Dll 的详细信息，请参阅该主题"有关动态链接库中"在 Microsoft Windows SDK 文档中。

实现 IHV 扩展 DLL 时，请参阅以下准则。

-   Wlanihv.h 中声明的结构和 IHV 扩展 DLL 的引用的函数原型。

-   IHV 扩展 DLL 必须实现[ *Dot11ExtIhvGetVersionInfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_get_version_info)并[ *Dot11ExtIhvInitService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_service)函数。 此外，这些函数都必须通过使用以生成的 DLL 的模块定义 (.def) 文件导出。 操作系统将通过这些函数的地址解析**GetProcAddress**函数。 有关详细信息**GetProcAddress**，请参阅 Windows SDK 文档。

-   IHV 扩展 DLL 必须实现所有 IHV 处理程序函数。 DLL 对这些函数返回的函数指针的列表，当操作系统将调用[ *Dot11ExtIhvInitService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_service)函数。

    有关 IHV 处理程序函数的详细信息，请参阅[本机 802.11 IHV 处理程序函数](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-handler-functions)。

-   对于 Windows Vista，IHV 扩展 DLL 必须支持接口版本号为零。 当[ *Dot11ExtIhvGetVersionInfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_get_version_info)是调用，该 DLL 必须定义所需的最低和最大受支持的界面版本为零。

 

 





