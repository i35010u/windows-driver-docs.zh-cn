---
title: 模拟
description: 模拟
keywords:
- 安全 WDK 文件系统，添加安全检查
- 安全检查 WDK 文件系统，模拟
- 模拟 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 741b5ffcdcf9a2f42aea940d5304cd86018552f1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816777"
---
# <a name="impersonation"></a>模拟


## <span id="ddk_impersonation_if"></span><span id="DDK_IMPERSONATION_IF"></span>


某些文件系统可能发现代表原始调用方执行操作非常有用。 例如，在打开文件时，网络文件系统可能需要捕获调用方的安全信息，以便可以使用适当的凭据执行后续操作。 毫无疑问，这种类型的功能在文件系统和特定应用程序中都很有用。

模拟所需的关键例程包括：

-   [**PsImpersonateClient**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-psimpersonateclient) [**SeImpersonateClientEx**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seimpersonateclientex)--启动模拟。 除非指示特定的线程，否则将在当前线程上下文中执行模拟。

-   **PsRevertToSelf**--在当前线程上下文中终止模拟。

-   [**PsReferencePrimaryToken**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-psreferenceprimarytoken)--在主 (进程中保存对指定进程) 标记的引用。 此函数可用于捕获系统上任何进程的标记。

-   [**PsDereferencePrimaryToken**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-psdereferenceprimarytoken)--释放对以前引用的主要令牌的引用。

-   [**SeCreateClientSecurityFromSubjectContext**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-secreateclientsecurityfromsubjectcontext)--返回一个客户端安全上下文，该上下文适用于在 **IRP \_ MJ \_ 创建** 处理期间提供给 FSD 的使用者上下文模拟 (，例如) 。

-   [**SeCreateClientSecurity**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-secreateclientsecurity)--基于系统上的现有线程的安全凭据创建客户端安全上下文。

-   **ImpersonateSecurityContext**--在内核安全服务 ksecdd.sys 中模拟安全上下文。

-   **RevertSecurityContext**--在内核安全服务 ksecdd.sys 中终止模拟。

模拟是实现的直接顺序。 下面的代码示例演示了基本模拟：

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

文件系统开发人员可以使用此模拟代码的许多变体，但这提供了一种基本的方法说明。

 

