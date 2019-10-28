---
title: 模拟
description: 模拟
ms.assetid: 368c6741-b51a-4629-8ae6-a7848c07c0fc
keywords:
- 安全 WDK 文件系统，添加安全检查
- 安全检查 WDK 文件系统，模拟
- 模拟 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e7ec8a6d06b6487c135b49f515eab9afa3226a3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841207"
---
# <a name="impersonation"></a>模拟


## <span id="ddk_impersonation_if"></span><span id="DDK_IMPERSONATION_IF"></span>


某些文件系统可能发现代表原始调用方执行操作非常有用。 例如，在打开文件时，网络文件系统可能需要捕获调用方的安全信息，以便可以使用适当的凭据执行后续操作。 毫无疑问，这种类型的功能在文件系统和特定应用程序中都很有用。

模拟所需的关键例程包括：

-   [**PsImpersonateClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-psimpersonateclient) [**SeImpersonateClientEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seimpersonateclientex)--启动模拟。 除非指示特定的线程，否则将在当前线程上下文中执行模拟。

-   **PsRevertToSelf**--在当前线程上下文中终止模拟。

-   [**PsReferencePrimaryToken**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-psreferenceprimarytoken)--保留对指定进程的主（进程）令牌的引用。 此函数可用于捕获系统上任何进程的标记。

-   [**PsDereferencePrimaryToken**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-psdereferenceprimarytoken)--释放对以前引用的主要令牌的引用。

-   [**SeCreateClientSecurityFromSubjectContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-secreateclientsecurityfromsubjectcontext)--返回一个客户端安全上下文，该上下文可用于从主题上下文模拟（例如，在**IRP\_MJ\_创建**处理期间提供给 FSD。

-   [**SeCreateClientSecurity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-secreateclientsecurity)--基于系统上的现有线程的安全凭据创建客户端安全上下文。

-   **ImpersonateSecurityContext**--模拟 ksecdd （内核安全服务）中的安全上下文。

-   **RevertSecurityContext**--在 ksecdd 中终止模拟，即内核安全服务。

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

 

 




