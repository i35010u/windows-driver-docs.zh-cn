---
title: Impersonation
description: Impersonation
ms.assetid: 368c6741-b51a-4629-8ae6-a7848c07c0fc
keywords:
- 安全 WDK 文件系统，添加安全检查
- 安全检查 WDK 文件系统中，模拟
- 模拟 WDK 的文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c01fda410e546f57488f0effc9c614e5acd1ce0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375690"
---
# <a name="impersonation"></a>Impersonation


## <span id="ddk_impersonation_if"></span><span id="DDK_IMPERSONATION_IF"></span>


某些文件系统可能会发现可以代表原始调用方执行操作。 例如，网络文件系统可能需要捕获数据时调用方的安全信息，以便可以使用相应的凭据执行后续操作打开文件。 毫无疑问，有许多其他特殊的情况下此类功能非常有用，同时也与特定的应用程序在文件系统中。

对于模拟需要包括关键的例程：

-   [**PsImpersonateClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-psimpersonateclient) [**SeImpersonateClientEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-seimpersonateclientex)-启动模拟。 指示特定线程，除非是在当前线程上下文中完成模拟。

-   **PsRevertToSelf**-终止当前线程上下文中的模拟。

-   [**PsReferencePrimaryToken**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-psreferenceprimarytoken)-指定进程的主 （进程） 令牌上保留的引用。 此函数可用于捕获系统上的任何进程的标记。

-   [**PsDereferencePrimaryToken**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-psdereferenceprimarytoken)-释放以前引用的主令牌上的引用。

-   [**SeCreateClientSecurityFromSubjectContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-secreateclientsecurityfromsubjectcontext)-返回客户端用于从使用者上下文的模拟安全上下文 (提供给期间 FSD **IRP\_MJ\_创建**处理，例如)。

-   [**SeCreateClientSecurity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-secreateclientsecurity)-创建客户端安全上下文基于在系统上的现有线程的安全凭据。

-   **ImpersonateSecurityContext**-模拟安全上下文中 ksecdd.sys，内核安全服务。

-   **RevertSecurityContext**-终止 ksecdd.sys，内核安全服务中的模拟。

模拟是简单直接的实现。 下面的代码示例演示了基本模拟：

```cpp
NTSTATUS PerformSpecialTask(IN PFSD_CONTEXT Context)
{
  BOOLEAN CopyOnOpen;
  BOOLEAN EffectiveOnly;
  SECURITY_IMPERSONATION_LEVEL ImpersonationLevel;
  NTSTATUS Status;
  PACCESS_TOKEN oldToken;

  //
  // We need to perform a task in the system process context
  //
  if (NULL == Context->SystemProcess) {

    return STATUS_NO_TOKEN;

  }

  //
  // Save the existing token, if any (otherwise NULL)
  //
  oldToken = PsReferenceImpersonationToken(PsGetCurrentThread(),
                                           &CopyOnOpen,
                                           &EffectiveOnly,
                                           &ImpersonationLevel);

  Status = PsImpersonateClient( PsGetCurrentThread(),
                                Context->SystemProcess,
                                TRUE,
                                TRUE,
                                SecurityImpersonation);
  if (!NT_SUCCESS(Status)) {

    if (oldToken)
        PsDereferenceImpersonationToken(oldToken);
    return Status;

  }

  //
  // Perform task - whatever it is
  //


  //
  // Restore to previous impersonation level
  //
  if (oldToken) {
    Status = PsImpersonateClient(PsGetCurrentThread(),
                                 oldToken,
                                 CopyOnOpen,
                                 EffectiveOnly,
                                 ImpersonationLevel);

    if (!NT_SUCCESS(Status)) {
      //
      // This is bad - we can't restore, we can't leave it this way 
      //
      PsRevertToSelf();
    }
    PsDereferenceImpersonationToken(oldToken);
  } else {
    PsRevertToSelf();
  }

  return Status;
}
```

可用于文件系统的开发人员的许多此模拟代码的变体，但这提供了该技术的基本说明。

 

 




