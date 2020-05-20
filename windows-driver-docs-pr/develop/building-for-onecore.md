---
title: 针对 OneCore 生成
description: 可以针对 Windows 10 之前的版本和 OneCore 版本生成单个二进制文件。
ms.assetid: ee46801a-4fa5-465a-aa81-5e76eb83d315
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: bf8bf6e343b296b6dcb7ab13135d2fe148a79a36
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235404"
---
# <a name="building-for-onecore"></a>针对 OneCore 进行构建

使用 Visual Studio 生成适用于 Windows 10 的用户模式代码时，可以自定义针对特定版本的 Windows 的链接器选项。  请考虑下列因素：

* 生成的二进制文件是否只应在最新版本的 Windows 上运行？  还是应该在 Windows 7 等早期版本上运行？  

* 项目是否有任何 [UWP](https://docs.microsoft.com/windows/uwp/get-started/whats-a-uwp) 依赖项？

例如，默认情况下，创建新的 UMDF v2 驱动程序项目时，Visual Studio 会链接到 `OneCoreUAP.lib`。  这会生成一个在最新版本的 Windows 上运行的二进制文件，且允许添加 UWP 功能。

但是，根据要求的不同，可以选择改为链接到 `OneCore.lib`。 下表显示了适用于每个库的方案：

|库|方案|
|-|-|
|`OneCore.lib`|Windows 7 及更高版本的所有版本，不支持 UWP|
|`OneCoreUAP.lib`|Windows 7 及更高版本、Windows 10 的 UWP 版本（Desktop、IoT、HoloLens，但不包括 Nano Server）|

>[!NOTE]
>若要更改 Visual Studio 中的链接器选项，请选择项目属性，然后导航至“链接器”->“输入”->“其他依赖项”。

Windows API 的一个子集可以干净地编译，但在非 Desktop 的 OneCore 版本（例如 Mobile 或 IoT）上返回运行时错误。

例如，[**InstallApplication**](https://docs.microsoft.com/windows/desktop/api/appmgmt/nf-appmgmt-installapplication) 函数在非 Desktop 的 OneCore 版本中会返回 `ERROR_ NOT_SUPPORTED`。  [ApiValidator](validating-universal-drivers.md) 工具也会报告这些问题。 下一部分将介绍如何解决这些问题。

## <a name="fixing-apivalidator-errors-by-using-isapisetimplemented"></a>使用 [**IsApiSetImplemented**](https://docs.microsoft.com/windows/desktop/api/apiquery2/nf-apiquery2-isapisetimplemented) 修复 ApiValidator 错误

如果代码调用非通用 API，可能会显示以下 [ApiValidator](validating-universal-drivers.md) 错误：

* `Error: <Binary Name> has unsupported API call to <Module Name><Api Name>`
    
    如果应用或基准驱动程序需要在 Windows 10 以及早期版本的 Windows 上运行，则必须删除上述类别中的 API 调用。

* `Error: <Binary Name> has a dependency on <Module Name><Api Name> but is missing: IsApiSetImplemented("<contract-name-for-Module>)`
    
    上述类别中的 API 调用编译良好，但在运行时可能表现不符合预期，具体取决于目标操作系统。 若要传递 [Windows 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-windows-drivers)的 [API 分层要求](api-layering.md)，请使用 [IsApiSetImplemented](https://docs.microsoft.com/windows/desktop/api/apiquery2/nf-apiquery2-isapisetimplemented) 包装这些调用。

这使你能够编译代码而不出错。  然后在运行时，如果目标计算机没有所需的 API，则 [**IsApiSetImplemented**](https://docs.microsoft.com/windows/desktop/api/apiquery2/nf-apiquery2-isapisetimplemented) 将返回 FALSE。

以下代码示例说明了如何执行此操作。

## <a name="code-sample-direct-usage-of-api-without-evaluating-for-existence"></a>代码示例：直接使用 API，无需评估是否存在

此代码在早于 Windows 10 的 Windows 版本上运行良好，但在 Windows 10 的 OneCore 版本上运行会导致 WTSEnumerateSessions 失败：78 或 ERROR_CALL_NOT_IMPLEMENTED 120 (0x78)。

此代码示例不符合 Windows 驱动程序的 [API 分层](api-layering.md)要求，出现了以下 [ApiValidator](validating-universal-drivers.md) 错误：

```cpp
ApiValidation: Error: FlexLinkTest.exe has a dependency on 'wtsapi32.dll!WTSEnumerateSessionsW' but is missing: IsApiSetImplemented("ext-ms-win-session-wtsapi32-l1-1-0")
ApiValidation: Error: FlexLinkTest.exe has a dependency on 'wtsapi32.dll!WTSFreeMemory' but is missing: IsApiSetImplemented("ext-ms-win-session-wtsapi32-l1-1-0")
ApiValidation: NOT all binaries are Universal
```
代码如下：

```cpp
#include <windows.h>
#include <stdio.h>
#include <Wtsapi32.h>

int __cdecl wmain(int /* argc */, PCWSTR /* argv */ [])
{
    PWTS_SESSION_INFO pInfo = {};
    DWORD count = 0;

    if (WTSEnumerateSessionsW(WTS_CURRENT_SERVER_HANDLE, 0, 1, &pInfo, &count))
    {
        wprintf(L"SessionCount = %d\n", count);

        for (ULONG i = 0; i < count; i++)
        {
            PWTS_SESSION_INFO pCurInfo = &pInfo[i];
            wprintf(L"    %s: ID = %d, state = %d\n", pCurInfo->pWinStationName, pCurInfo->SessionId, pCurInfo->State);
        }

        WTSFreeMemory(pInfo);
    }
    else
    {
        wprintf(L"WTSEnumerateSessions failure : %x\n", GetLastError());
    } 

    return 0;
}
```

## <a name="code-sample-direct-usage-of-api-after-evaluating-for-existence"></a>代码示例：评估是否存在后直接使用 API

此示例演示如何调用 [**IsApiSetImplemented**](https://docs.microsoft.com/windows/desktop/api/apiquery2/nf-apiquery2-isapisetimplemented)。 此示例符合 Windows 驱动程序的 [API 分层](api-layering.md)要求，生成了以下 [ApiValidator](validating-universal-drivers.md) 输出：

```cpp
ApiValidation: All binaries are Universal
```

代码如下：

```cpp
#include <windows.h>
#include <stdio.h>
#include <Wtsapi32.h>

int __cdecl wmain(int /* argc */, PCWSTR /* argv */ [])
{
    PWTS_SESSION_INFO pInfo = {};
    DWORD count = 0;

    if (!IsApiSetImplemented("ext-ms-win-session-wtsapi32-l1-1-0"))
    {
        wprintf(L"IsApiSetImplemented on ext-ms-win-session-wtsapi32-l1-1-0 returns FALSE\n");
    }
    else
    {
        if (WTSEnumerateSessionsW(WTS_CURRENT_SERVER_HANDLE, 0, 1, &pInfo, &count))
        {
            wprintf(L"SessionCount = %d\n", count);

            for (ULONG i = 0; i < count; i++)
            {
                PWTS_SESSION_INFO pCurInfo = &pInfo[i];
                wprintf(L"    %s: ID = %d, state = %d\n", pCurInfo->pWinStationName, pCurInfo->SessionId, pCurInfo->State);
            }

            WTSFreeMemory(pInfo);
        }
        else
        {
            wprintf(L"WTSEnumerateSessions failure : %x\n", GetLastError());
        }
    }

    return 0;
}
```

## <a name="recommended-actions"></a>建议的操作

* 查看上面的链接器选项并相应地更新 Visual Studio 项目。
* 使用 WDK 中的 [ApiValidator](validating-universal-drivers.md) 工具。  在 Visual Studio 中生成驱动程序时该工具会自动运行。
* 使用运行时测试验证用户模式代码是否按照预期在非 Desktop 的 OneCore 版本上运行。  请注意，存根 API 可能会生成不同的错误代码。

## <a name="see-also"></a>另请参阅

* [验证 Windows 驱动程序](validating-windows-drivers.md)
* [OneCore](https://docs.microsoft.com/windows-hardware/get-started/what-s-new-in-windows)

<!--API BOILERPLATE: Compiles using OneCore.lib but returns ERROR_CALL_NOT_IMPLEMENTED on non-Desktop OneCore editions.-->
