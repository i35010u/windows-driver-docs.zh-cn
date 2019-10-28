---
title: 本机 802.11 IHV 扩展 DLL 实现指导原则
description: 本机 802.11 IHV 扩展 DLL 实现指导原则
ms.assetid: ef13de2a-3510-46c5-afb6-0bf1002af5ca
keywords:
- IHV 扩展 DLL WDK 本机802.11，实现指南
- 本机 802.11 IHV 扩展 DLL WDK，实现指南
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfd96a5f727bf888975d2abf8c04834da27be2f3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839643"
---
# <a name="native-80211-ihv-extensions-dll-implementation-guidelines"></a>本机 802.11 IHV 扩展 DLL 实现指导原则




 

IHV 扩展 DLL 实现为运行时动态链接库（DLL）。 有关 Dll 的详细信息，请参阅 Microsoft Windows SDK 文档中的主题 "关于动态链接库"。

实现 IHV 扩展 DLL 时，请参阅以下准则。

-   在 Wlanihv 中声明了 IHV 扩展 DLL 所引用的结构和函数原型。

-   IHV 扩展 DLL 必须实现[*Dot11ExtIhvGetVersionInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_get_version_info)和[*Dot11ExtIhvInitService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_service)函数。 此外，这些函数必须通过用于生成 DLL 的模块定义（.def）文件导出。 操作系统通过**GetProcAddress**函数解析这些函数的地址。 有关**GetProcAddress**的详细信息，请参阅 Windows SDK 文档。

-   IHV 扩展 DLL 必须实现所有 IHV 处理程序函数。 当操作系统调用[*Dot11ExtIhvInitService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_service)函数时，DLL 返回这些函数的函数指针列表。

    有关 IHV 处理程序函数的详细信息，请参阅[本机 802.11 IHV 处理程序函数](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-handler-functions)。

-   对于 Windows Vista，IHV 扩展 DLL 必须支持接口版本零。 调用[*Dot11ExtIhvGetVersionInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_get_version_info)时，DLL 必须将支持的最小和最大接口版本定义为零。

 

 





