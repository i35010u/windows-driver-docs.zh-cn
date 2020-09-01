---
title: 检查正在进行的安装
description: 检查正在进行的安装
ms.assetid: 9630a22e-65df-41f1-bfaf-ef4df9ca8aed
keywords:
- 正在进行的安装 WDK
- 正在检查正在进行的安装
- 验证正在进行的安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b760cca9a05cd23bbd7e42bb06fd0b6197ad547
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097159"
---
# <a name="checking-for-in-progress-installations"></a>检查正在进行的安装

*设备安装应用程序*应该确定在执行其他安装活动之前是否正在进行安装。 为了做出此决定，设备安装应用程序应调用 [**CMP_WaitNoPendingInstallEvents**](/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_waitnopendinginstallevents)，通常为零超时值。 如果此函数的返回值指示其他安装活动处于挂起状态 (例如，"发现新硬件" 向导可能处于活动状态) ，则设备安装应用程序应该退出。

若要使 *设备安装应用程序* 与不支持 **CMP_WaitNoPendingInstallEvents**的平台兼容，应用程序应包含以下代码：

```cpp
BOOL
IsDeviceInstallInProgress (VOID)
{
    HMODULE hModule;
    CMP_WAITNOPENDINGINSTALLEVENTS_PROC pCMP_WaitNoPendingInstallEvents;

    hModule = GetModuleHandle(TEXT("setupapi.dll"));
    if(!hModule)
    {
        // Should never happen since we're linked to SetupAPI, but...
        return FALSE;
    }

    pCMP_WaitNoPendingInstallEvents =
        (CMP_WAITNOPENDINGINSTALLEVENTS_PROC)GetProcAddress(hModule,
                                             "CMP_WaitNoPendingInstallEvents");
    if(!pCMP_WaitNoPendingInstallEvents)
    {
        // We're running on a release of the operating system that doesn't supply this function.
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
        // We don't want to start right now.  Instead, our
        // device co-installer will invoke this application
        // (if necessary) during finish-install processing.
        //
        return -1;
    }
    .
    .
}
```

此代码的使用基于在平台不支持 **CMP_WaitNoPendingInstallEvents**的前提下，如果安装活动正在进行，则平台不会启动自动运行。

有关此代码的示例用法，请参阅 Windows 驱动程序工具包 (WDK) 下的 *src \\ general \\ toaster* 子目录下的 toaster 安装包。