---
title: 检查正在进行安装
description: 检查正在进行安装
ms.assetid: 9630a22e-65df-41f1-bfaf-ef4df9ca8aed
keywords:
- 正在安装 WDK
- 检查正在进行安装
- 验证正在进行安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d97c6d217eeeaa76d29c1730ffb33d8791d8d247
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533143"
---
# <a name="checking-for-in-progress-installations"></a>检查正在进行安装





你*设备安装应用程序*应确定安装的其他活动是否正在进行中之前执行其安装。 若要做出此判断，设备安装应用程序应调用[ **CMP_WaitNoPendingInstallEvents**](https://msdn.microsoft.com/library/windows/hardware/ff537916)，通常使用超时值为零。 如果此函数的返回值指示其他安装活动处于挂起状态 （例如，发现新硬件向导可能处于活动状态），设备安装应用程序应退出。

若要使你*设备安装应用程序*与不支持的平台兼容**CMP_WaitNoPendingInstallEvents**，应用程序应包括下面的代码：

```cpp
BOOL
IsDeviceInstallInProgress (VOID)
{
    HMODULE hModule;
    CMP_WAITNOPENDINGINSTALLEVENTS_PROC pCMP_WaitNoPendingInstallEvents;

    hModule = GetModuleHandle(TEXT("setupapi.dll"));
    if(!hModule)
    {
        // Should never happen since we&#39;re linked to SetupAPI, but...
        return FALSE;
    }

    pCMP_WaitNoPendingInstallEvents = 
        (CMP_WAITNOPENDINGINSTALLEVENTS_PROC)GetProcAddress(hModule,
                                             "CMP_WaitNoPendingInstallEvents");
    if(!pCMP_WaitNoPendingInstallEvents)
    {
        // We&#39;re running on a release of the operating system that doesn&#39;t supply this function.
        // Trust the operating system to suppress AutoRun when appropriate.
        return FALSE;
    }
    return (pCMP_WaitNoPendingInstallEvents(0) == WAIT_TIMEOUT);
}

int
__cdecl
_tmain(IN int argc, IN PTCHAR argv[])
{
    if(IsDeviceInstallInProgress()) {
        //
        // We don&#39;t want to start right now.  Instead, our 
        // device co-installer will invoke this application 
        // (if necessary) during finish-install processing.
        //
        return -1;
    }
    .
    .
}
```

使用此代码为基础的前提，如果一个平台不支持**CMP_WaitNoPendingInstallEvents**，该平台不会启动自动运行，如果正在安装活动。

此代码的使用示例，请参阅下的 toaster 安装包*src\\常规\\toaster*子目录的 Windows Driver Kit (WDK)。

 

 





