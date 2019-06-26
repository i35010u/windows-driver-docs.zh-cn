---
title: 安全标识符
description: 安全标识符
ms.assetid: e4c39d83-6f32-406c-b8d5-d41305a8976f
keywords:
- 安全描述符 WDK 文件系统，安全标识符
- 描述符 WDK 文件系统，安全标识符
- WDK 的文件系统的安全标识符
- Sid WDK 的文件系统
- 已知标识符 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2255ce63be01547495603b78260b5ad64c6e30fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371347"
---
# <a name="security-identifier"></a>安全标识符


## <span id="ddk_security_identifier_if"></span><span id="DDK_SECURITY_IDENTIFIER_IF"></span>


安全标识符用于通过 Windows 作为最终值将安全实体与另一个区分开来。 例如，唯一安全标识符分配给为系统上的单个用户创建的每个新帐户。 对于文件系统，实际使用只有此 SID。

下图演示了安全标识符结构。

![说明安全标识符结构的关系图](images/fssecurity-02.png)

唯一的 Sid，除了 Windows 系统定义一的组已知的标识符。 例如，本地管理员是此类已知的 SID。 Windows 提供了 Sid 和用户之间进行转换的内核环境中的名称在内核机制。 Ksecdd 驱动程序，可以通过使用用户模式下的帮助程序服务来实现这些函数中提供了这些函数调用。 相应地，其使用文件系统中的必须遵循与用户模式服务的通信的常用规则。 不能在分页文件 I/O 期间使用这些调用。

这些函数包括：

-   [**SecMakeSPN**](https://msdn.microsoft.com/library/windows/hardware/ff556584)— 创建与特定的安全服务提供商进行通信时可以使用一个服务提供程序名称字符串。

-   [**SecMakeSPNEx**](https://msdn.microsoft.com/library/windows/hardware/ff556585)— 的增强的版本**SecMakeSPN**。 此函数是 Microsoft Windows XP 和更高版本的 Windows 上可用。

-   [**SecMakeSPNEx2**](https://msdn.microsoft.com/library/windows/hardware/ff556592)— 的增强的版本**SecMakeSPNEx**。 此函数是 Windows Vista、 Windows Server 2008 和更高版本的 Windows 上可用。

-   [**SecLookupAccountSid**](https://msdn.microsoft.com/library/windows/hardware/ff556579)，给定一个 SID，此例程将返回帐户名称。 此函数是适用于 Windows XP 及更高版本。

-   [**SecLookupAccountName**](https://msdn.microsoft.com/library/windows/hardware/ff554795)— 给定帐户名称，此例程将检索 SID。 此函数是适用于 Windows XP 及更高版本。

-   [**SecLookupWellKnownSid**](https://msdn.microsoft.com/library/windows/hardware/ff556582)— 给定的已知 SID 类型，此例程将返回正确的 SID。 此函数是适用于 Windows Server 2003 及更高版本。

此外，任何内核驱动程序可能会使用以下标准运行时库例程来创建一个 SID:

-   [**RtlInitializeSid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-rtlinitializesid)— 缓冲区初始化为一个新的 SID。

-   [**RtlLengthSid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-rtllengthsid)— 确定给定缓冲区中存储的 SID 的大小。

-   [**RtlValidSid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-rtlvalidsid)— 确定给定的 SID 缓冲区是否是有效的格式化的缓冲区。

请注意， **RtlLengthSid**并**RtlValidSid**假定一个 SID 的 8 字节固定的标题已存在。 因此驱动程序应检查此最小长度为 SID 标头调用这些函数之前。

尽管有几个其他 RTL 函数，它们是必需的主函数，构造一个 SID 时。

下面的代码示例演示如何创建"本地系统"实体的 SID:

```cpp
{
    //
    // temporary stack-based storage for an SID
    //
    UCHAR sidBuffer[128];
    PISID localSid = (PISID) sidBuffer;
    SID_IDENTIFIER_AUTHORITY localSidAuthority = 
        SECURITY_NT_AUTHORITY;

    //
    // build the local system SID
    //
    RtlZeroMemory(sidBuffer, sizeof(sidBuffer));
 
    localSid->Revision = SID_REVISION;
    localSid->SubAuthorityCount = 1;
    localSid->IdentifierAuthority = localSidAuthority;
    localSid->SubAuthority[0] = SECURITY_LOCAL_SYSTEM_RID;
 
    //
    // make sure it is valid
    //
    if (!RtlValidSid(localSid)) {
        DbgPrint("no dice - SID is invalid\n");
        return(1);
    }
}
```

请注意，这可能还进行了使用更简单的函数**SecLookupWellKnownSid**在 Windows Server 2003 中引入的。

下面的代码示例演示如何创建使用一个 SID **SecLookupWellKnownSid** "本地系统"实体的函数：

```cpp
{
    UCHAR sidBuffer[128];
    PISID localSid = (PISID) sidBuffer;
    SIZE_T sidSize;
    status = SecLookupWellKnownSid(WinLocalSid,
                                   &localSid,
                                   sizeof(sidBuffer),
                                   &sidSize);

    if (!NT_SUCCESS(status)) {
      //
      // error handling
      //
    }
  }
```

尽管后一种代码优先，任一种方法都有效。 请注意，这些代码示例使用的本地缓冲区存储 SID。 不能在当前调用上下文外部使用这些缓冲区。 如果 SID 缓冲区需要在不变，则应从池内存分配缓冲区。

 

 




