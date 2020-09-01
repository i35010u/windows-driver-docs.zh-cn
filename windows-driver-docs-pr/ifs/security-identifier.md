---
title: 安全标识符
description: 安全标识符
ms.assetid: e4c39d83-6f32-406c-b8d5-d41305a8976f
keywords:
- 安全描述符 WDK 文件系统、安全标识符
- 描述符文件系统、安全标识符
- 安全标识符 WDK 文件系统
- Sid WDK 文件系统
- 众所周知的标识符 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22a789c09ddaf8028fdf584cf650c90dea841669
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065930"
---
# <a name="security-identifier"></a>安全标识符


## <span id="ddk_security_identifier_if"></span><span id="DDK_SECURITY_IDENTIFIER_IF"></span>


Windows 将安全标识符用作权威性值，以区分不同的安全实体。 例如，为系统上的单个用户创建的每个新帐户分配唯一安全标识符。 对于文件系统，只实际使用此 SID。

下图说明了安全标识符的结构。

![说明安全标识符结构的关系图](images/fssecurity-02.png)

除了唯一的 Sid，Windows 系统还定义一组众所周知的标识符。 例如，本地管理员是众所周知的 SID。 Windows 提供了内核内的机制，用于在内核环境内的 Sid 和用户名之间进行转换。 Ksecdd 驱动程序中提供了这些函数调用，该驱动程序使用用户模式 helper 服务实现这些功能。 因此，它们在文件系统中的使用必须遵循与用户模式服务通信的常用规则。 在分页文件 i/o 期间不能使用这些调用。

这些函数包括：

-   [**SecMakeSPN**](/previous-versions/ff556584(v=vs.85))-创建可在与特定安全服务提供程序通信时使用的服务提供程序名称字符串。

-   [**SecMakeSPNEx**](/previous-versions/ff556585(v=vs.85))— **SecMakeSPN**的扩充版本。 此功能在 Microsoft Windows XP 和更高版本的 Windows 上可用。

-   [**SecMakeSPNEx2**](/previous-versions/ff556592(v=vs.85))— **SecMakeSPNEx**的扩充版本。 此功能在 Windows Vista、Windows Server 2008 和更高版本的 Windows 上可用。

-   [**SecLookupAccountSid**](/previous-versions/ff556579(v=vs.85))—给定 SID 后，此例程将返回帐户名称。 此功能在 Windows XP 和更高版本上可用。

-   [**SecLookupAccountName**](/previous-versions/ff554795(v=vs.85))—在给定帐户名称的情况下，此例程将检索 SID。 此功能在 Windows XP 和更高版本上可用。

-   [**SecLookupWellKnownSid**](/previous-versions/ff556582(v=vs.85))—如果给定一个已知的 sid 类型，此例程将返回正确的 sid。 此功能在 Windows Server 2003 及更高版本中可用。

此外，任何内核驱动程序都可以使用以下标准运行时库例程创建 SID：

-   [**RtlInitializeSid**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-rtlinitializesid)-初始化新 SID 的缓冲区。

-   [**RtlLengthSid**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-rtllengthsid)-确定存储在给定缓冲区中的 SID 大小。

-   [**RtlValidSid**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-rtlvalidsid)-确定给定的 SID 缓冲区是否为有效的格式化缓冲区。

请注意， **RtlLengthSid** 和 **RtlValidSid** 假设存在8字节的固定标头。 因此，在调用这些函数之前，驱动程序应该检查 SID 标头的最小长度。

尽管有多个 RTL 函数，但这些是构造 SID 时所需的主要功能。

下面的代码示例演示如何为 "local system" 实体创建 SID：

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

请注意，也可以使用 Windows Server 2003 中引入的更简单的函数 **SecLookupWellKnownSid** 来完成此操作。

下面的代码示例演示如何使用 **SecLookupWellKnownSid** 函数为 "local system" 实体创建 SID：

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

虽然这两种方法都是有效的，但这两种方法是首选的。 请注意，这些代码示例使用本地缓冲区来存储 SID。 在当前调用上下文外部不能使用这些缓冲区。 如果需要持久性 SID 缓冲区，应从池内存中分配缓冲区。

 

