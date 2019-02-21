---
title: 调试权限
description: 调试权限可让人调试它们否则不会有权访问的进程。
ms.assetid: f3ea9065-6d04-4629-88ed-85428f7915ca
keywords:
- 调试权限
- 调试权限，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c2ddfbf7f2d0e75b47727a6250402de47bd5c6e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533721"
---
# <a name="debug-privilege"></a>调试权限


调试权限可让人调试它们否则不会有权访问的进程。 例如，使用其令牌上启用了调试特权以用户身份运行的进程可以调试作为本地系统运行的服务。

## <span id="ddk_reading_and_writing_registers_and_flags_dbg"></span><span id="DDK_READING_AND_WRITING_REGISTERS_AND_FLAGS_DBG"></span>


调试权限是允许用户将调试器附加到进程或内核的安全策略设置。 管理员可以修改安全策略的用户组以包含或若要删除此功能。 在调试自己的应用程序开发人员不需要此用户权限。 谁正在调试系统组件或谁正在调试远程组件的开发人员将需要此用户权限。 此用户权限提供了对敏感和关键操作系统组件的完全访问权限。 默认情况下，此属性可用于具有管理员权限的用户。 具有管理员权限的用户可以启用此属性为其他用户组。

### <a name="span-idmodifyingdebugprivilegeforaprocessspanspan-idmodifyingdebugprivilegeforaprocessspanmodifying-debug-privilege-for-a-process"></a><span id="modifying_debug_privilege_for_a_process"></span><span id="MODIFYING_DEBUG_PRIVILEGE_FOR_A_PROCESS"></span>修改进程调试权限

下面的代码示例演示如何启用过程中的调试特权。 这使你能够调试不会否则有权访问其他进程。

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

 

 





