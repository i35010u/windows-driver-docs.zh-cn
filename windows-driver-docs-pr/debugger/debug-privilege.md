---
title: 调试特权
description: 调试权限允许他人调试他们无权访问的进程。
keywords:
- 调试权限
- 调试权限，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 048e05865649efae779cd08d79bb8f6831bd56b3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828255"
---
# <a name="debug-privilege"></a>调试特权


调试权限允许他人调试他们无权访问的进程。 例如，以用户身份启用了调试权限的用户身份运行的进程可以调试作为 "本地系统" 运行的服务。

## <span id="ddk_reading_and_writing_registers_and_flags_dbg"></span><span id="DDK_READING_AND_WRITING_REGISTERS_AND_FLAGS_DBG"></span>


调试权限是一种安全策略设置，它允许用户将调试器附加到进程或内核。 管理员可以修改用户组的安全策略，使其包括或删除此功能。 正在调试自己的应用程序的开发人员不需要此用户权限。 正在调试系统组件或正在调试远程组件的开发人员将需要此用户权限。 此用户特权提供对敏感和关键操作系统组件的完全访问权限。 默认情况下，将为具有管理员权限的用户启用此属性。 具有管理员权限的用户可以为其他用户组启用此属性。

### <a name="span-idmodifying_debug_privilege_for_a_processspanspan-idmodifying_debug_privilege_for_a_processspanmodifying-debug-privilege-for-a-process"></a><span id="modifying_debug_privilege_for_a_process"></span><span id="MODIFYING_DEBUG_PRIVILEGE_FOR_A_PROCESS"></span>修改进程的调试权限

下面的代码示例演示如何在进程中启用调试特权。 这使您可以调试其他无法访问的进程。

```cpp
//
//  SetPrivilege enables/disables process token privilege.
//
BOOL SetPrivilege(HANDLE hToken, LPCTSTR lpszPrivilege, BOOL bEnablePrivilege)
{
    LUID luid;
    BOOL bRet=FALSE;

    if (LookupPrivilegeValue(NULL, lpszPrivilege, &luid))
    {
        TOKEN_PRIVILEGE tp;

        tp.PrivilegeCount=1;
        tp.Privileges[0].Luid=luid;
        tp.Privileges[0].Attributes=(bEnablePrivilege) ? SE_PRIVILEGE_ENABLED: 0;
        //
        //  Enable the privilege or disable all privileges.
        //
        if (AdjustTokenPrivileges(hToken, FALSE, &tp, NULL, (PTOKEN_PRIVILEGES)NULL, (PDWORD)NULL))
        {
            //
            //  Check to see if you have proper access.
            //  You may get "ERROR_NOT_ALL_ASSIGNED".
            //
            bRet=(GetLastError() == ERROR_SUCCESS);
        }
    }
    return bRet;
}
```

下面的示例演示如何使用此函数：

```cpp
HANDLE hProcess=GetCurrentProcess();
HANDLE hToken;

if (OpenProcessToken(hProcess, TOKEN_ADJUST_PRIVILEGES, &hToken))
{
    SetPrivilege(hToken, SE_DEBUG_NAME, TRUE);
    CloseHandle(hToken);
}
```

 

 





