---
title: 智能卡微型驱动器概述
description: 智能卡微型驱动器概述
ms.assetid: B5047C79-F74E-44FA-ADE5-8716ABC9EB79
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e53ef8940237d98d22795f23e9d6f20892d0adc
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382685"
---
# <a name="smart-card-minidriver-overview"></a>智能卡微型驱动器概述


特定于卡的微型驱动程序是基本 CSP/KSP 中的最低逻辑接口层。 此微型驱动程序允许基本 CSP/KSP 和应用程序通过使用 SCRM 直接与特定类型的卡交互。

卡微型驱动程序是一个 DLL，用于导出此规范中定义的一组特定 Api。 对卡微型驱动程序的每次调用都包含指向提供上下文信息的 [**卡片 \_ 数据**](/previous-versions/dn468748(v=vs.85)) 结构的指针。 此上下文信息除了提供函数指针表之外，还提供一些状态信息，用于促进高层和卡微型驱动程序之间的通信。

有关此上下文结构的详细信息，请参阅 [**CardAcquireContext**](/previous-versions/dn468701(v=vs.85))。

## <a name="span-idrelated_documentspanspan-idrelated_documentspanspan-idrelated_documentspanrelated-document"></a><span id="Related_Document"></span><span id="related_document"></span><span id="RELATED_DOCUMENT"></span>相关文档


*Cardmod* C 头文件提供了与此规范相关的其他信息。 此文件包含 Microsoft 智能卡微型驱动程序 API 指定的函数原型和结构。 此 API 通过 Microsoft 加密提供程序开发工具包提供 (CPDK) 。

## <a name="span-idgeneral_design_guidelinesspanspan-idgeneral_design_guidelinesspanspan-idgeneral_design_guidelinesspangeneral-design-guidelines"></a><span id="General_Design_Guidelines"></span><span id="general_design_guidelines"></span><span id="GENERAL_DESIGN_GUIDELINES"></span>一般设计准则


-   卡微型驱动程序应作为 DLL 分发。
-   每个特定于智能卡的操作应该实现单个原子事务，除非另有说明。
-   应该实现一组标准化的宏级别操作。
-   逻辑卡文件系统对象应映射到其物理位置。
-   基于此新模型的卡应能够动态增加存储在卡上的任何文件。 对于只读卡且不能遵循此指导原则，微型驱动程序应遵循本规范中详细说明的只读卡的特定准则。
-   微型驱动程序从 CPDK 导入定义。 微型驱动程序头文件 (*Cardmod*) 包含用于实现此目的的 *Bcrypt* 。 实现必须通过 Microsoft Visual Studio 用于编译微型驱动程序的项目设置来解决此依赖关系。
-   插件或驱动程序的受保护进程要求

    -   要使 LSA 插件或驱动程序以受保护进程的形式成功加载，它必须满足以下条件：

        -   签名验证

            o 保护模式要求加载到 LSA 中的任何插件必须使用 Microsoft 签名进行数字签名。 因此，任何未签名的或第三方签名的插件都无法加载到 LSA 中。 此类插件的示例包括智能卡驱动程序、加密插件和密码筛选器等。

            o (诸如智能卡驱动程序之类的驱动程序的 LSA 插件) 需要进行数字签名。

            **注意**   [Windows 硬件兼容性计划](/windows-hardware/design/compatibility/index)提供了用于对 Windows 的驱动程序进行数字签名的唯一方法。 因此，请务必参考网站获取此信息。

             

    -   遵守 Microsoft 安全开发生命周期 (SDL) 过程指南。

        -   所有插件还需要遵守 [Microsoft 安全开发生命周期的适用部分 (SDL) –过程指南](/previous-versions/windows/desktop/cc307891(v=msdn.10)) 主题。 例如，请参阅附录 G 的 SDL 过程中所述的 " *不共享" 部分*。

        -   即使插件已使用 Microsoft 签名正确地进行签名，但不符合 SDL 流程可能会导致加载插件失败。

有关 SDL 的详细信息，请参阅 [Microsoft 安全开发生命周期 (SDL) –过程指南](/previous-versions/windows/desktop/cc307891(v=msdn.10))。

有关面向开发人员的准则的讨论，请参阅 [开发人员指南](developer-guidelines.md)

## <a name="span-idtransaction_managementspanspan-idtransaction_managementspanspan-idtransaction_managementspantransaction-management"></a><span id="Transaction_Management"></span><span id="transaction_management"></span><span id="TRANSACTION_MANAGEMENT"></span>事务管理


-   卡微型驱动程序应假设当调用方使用 SCRM 访问卡时，将处理事务。
-   卡微型驱动程序可以假设除 [**CardDeleteContext**](/previous-versions/dn468715(v=vs.85)) 之外的所有入口点都是通过保存卡事务来调用的。 在 **CardDeleteContext** 中不能采用这种方式，因为该卡可能已被删除或作为清理过程的一部分被调用。
-   单个进程中可以存在多个上下文。 在一个进程上调用 [**CardDeleteContext**](/previous-versions/dn468715(v=vs.85)) 不会阻止其他上下文正常运行。
-   处理卡的身份验证状态也是调用方的责任，而不是卡微型驱动程序。

## <a name="span-idconventionsspanspan-idconventionsspanspan-idconventionsspanconventions"></a><span id="Conventions"></span><span id="conventions"></span><span id="CONVENTIONS"></span>规范


### <a name="span-idstrings__unicode_and_ansispanspan-idstrings__unicode_and_ansispanspan-idstrings__unicode_and_ansispanstrings-unicode-and-ansi"></a><span id="Strings__UNICODE_and_ANSI"></span><span id="strings__unicode_and_ansi"></span><span id="STRINGS__UNICODE_AND_ANSI"></span>字符串： UNICODE 和 ANSI

在应用程序级别，字符串通常作为用户界面的元素出现（直接或间接）。 因此，通常必须将其本地化 (翻译为用户的语言) 以便能够理解。 出于此原因，大多数应用程序使用的字符串类型是双字节 (即 UNICODE) 以容纳不同的字符集。

不过，智能卡可在资源最少的情况下运行，只需很少的选项来命名目录、文件、用户等。 字符串的字符集为单字节 ANSI，这提供了更简洁的字符串数据表示形式。

相应地，与卡微型驱动程序的字符串缓冲区应为单字节 ANSI，并根据需要从该字符类型转换到和从此字符类型进行转换，必须在微型驱动程序的外部执行。

### <a name="span-id_error_handlingspanspan-id_error_handlingspanspan-id_error_handlingspan-error-handling"></a><span id="_Error_Handling"></span><span id="_error_handling"></span><span id="_ERROR_HANDLING"></span> 错误处理

若要确保对卡微型驱动程序进行一致的错误处理、对失败的响应以及一致的行为，请遵循以下约定：

-   所有 NULL 和无效参数（包括错误标志）都返回放弃 \_ E \_ 无效 \_ 参数。
-   所有不正确的 PIN 或带有错误密钥的尝试返回放弃， \_ \_ \_ CHV 错误。
-   如果发生一般故障，Api 将返回意外的放弃 \_ E \_ 。

此外，以下部分中描述的函数所返回的错误应来自放弃 \_ \* 类别 (*winerror.h*) 。 例如，我们建议你使用放弃 \_ E \_ 无效 \_ 参数 (0x80100004) 而不是错误 \_ \_ (0x00000057) 的参数无效。

**注意**   如果无法从卡读取文件，因为 i/o 错误，或某些其他无法恢复的数据问题与卡上该文件的实际存在无关，则 Microsoft 建议返回放弃 \_ E \_ COMM \_ 数据 \_ 丢失。

如果 \_ \_ \_ 在这种情况下返回的放弃 E 文件未 \_ 找到为伞错误代码，则会提供误导性的调试信息。

 

## <a name="span-idauthentication_and_authorizationspanspan-idauthentication_and_authorizationspanspan-idauthentication_and_authorizationspanauthentication-and-authorization"></a><span id="Authentication_and_Authorization"></span><span id="authentication_and_authorization"></span><span id="AUTHENTICATION_AND_AUTHORIZATION"></span>身份验证和授权


从版本6开始，微型驱动程序接口将 PIN 的概念扩展到超过传统的字母数字字符串。 有关详细信息，请参阅 \_ 本规范后面的 " (枚举) 的机密类型"。

## <a name="span-idhandling_memory_allocationsspanspan-idhandling_memory_allocationsspanspan-idhandling_memory_allocationsspanhandling-memory-allocations"></a><span id="Handling_Memory_Allocations"></span><span id="handling_memory_allocations"></span><span id="HANDLING_MEMORY_ALLOCATIONS"></span>处理内存分配


此规范中的所有分配内存缓冲区的 API 元素都是通过调用 [**PFN \_ CSP \_ 分配**](/previous-versions/dn468763(v=vs.85))来实现的。 因此，任何此类内存缓冲区都必须通过调用 [**PFN \_ CSP \_ **](/previous-versions/dn468767(v=vs.85))释放。

卡微型驱动程序执行的任何内存分配都应该通过使用 [**PFN \_ csp \_ 分配**](/previous-versions/dn468763(v=vs.85)) 或 [**PFN \_ csp \_ REALLOC**](/previous-versions/dn468770(v=vs.85))来完成。

## <a name="span-idcachingspanspan-idcachingspanspan-idcachingspancaching"></a><span id="Caching"></span><span id="caching"></span><span id="CACHING"></span>缓存


基本 CSP/KSP 中的卡接口层实现了数据缓存，以最大程度地减少必须写入或读取数据的数据量。 数据缓存还可用于卡微型驱动程序，以通过 [**卡 \_ 数据**](/previous-versions/dn468748(v=vs.85)) 结构中的函数指针来使用，卡微型驱动程序应使用这些指针通过缓存存储在卡上的内部数据文件来提高性能。

数据缓存需要对卡的写访问权限才能将缓存新鲜度计数器持久保存到卡。 如果不可行将数据写入到卡，微型驱动程序可以控制数据缓存。

有关如何控制数据缓存的详细信息，请参阅 \_ \_ \_ 本规范后面的 [**CardGetProperty**](/previous-versions/dn468729(v=vs.85)) 中的 CP 卡缓存模式属性的定义。

## <a name="span-idmandatory_version_checkingspanspan-idmandatory_version_checkingspanspan-idmandatory_version_checkingspanmandatory-version-checking"></a><span id="Mandatory_Version_Checking"></span><span id="mandatory_version_checking"></span><span id="MANDATORY_VERSION_CHECKING"></span>强制版本检查


所有卡微型驱动程序必须实现版本检查。 [**卡 \_ 数据**](/previous-versions/dn468748(v=vs.85))结构的版本是调用方想要支持的版本与卡微型驱动程序可以实际支持的版本之间的协商。

### <a name="span-idcard_data_version_checksspanspan-idcard_data_version_checksspanspan-idcard_data_version_checksspancard_data-version-checks"></a><span id="CARD_DATA_Version_Checks"></span><span id="card_data_version_checks"></span><span id="CARD_DATA_VERSION_CHECKS"></span>卡 \_ 数据版本检查

将最低版本定义为卡微型驱动程序上下文结构的最低版本 (即，支持的 [**卡 \_ 数据**](/previous-versions/dn468748(v=vs.85)) 结构) ，并将当前版本定义为此卡微型驱动程序设计为的级别，并将所有微型驱动程序结构项保证为在 [**CardAcquireContext**](/previous-versions/dn468701(v=vs.85))成功返回时有效。 当前版本必须大于或等于最小版本，并小于或等于 \_ \_ \_ 在 *CARDMOD*中定义的卡数据当前版本。

调用应用程序调用 [**CardAcquireContext**](/previous-versions/dn468701(v=vs.85))时，它指定要加载的所需版本。 此请求的版本在[**卡 \_ 数据**](/previous-versions/dn468748(v=vs.85))结构的**dwVersion**成员中设置。

如果请求的版本低于卡微型驱动程序支持的最低版本，则 [**CardAcquireContext**](/previous-versions/dn468701(v=vs.85)) 必须返回修订不匹配错误 (参见下面的示例代码) 。

如果请求的版本至少与最低版本相同，则卡微型驱动程序应将 **dwVersion** 成员设置为它可支持的最高版本，该版本小于或等于请求的版本。

下面的示例代码演示了检查版本时的预期卡微型驱动程序行为。 假设此项位于 **CardAcquireContext** 函数的正文中。 *pCardData* 是指向传递给此调用的 [**卡 \_ 数据**](/previous-versions/dn468748(v=vs.85)) 结构的指针。

```ManagedCPlusPlus
#define MINIMUM_VERSION_SUPPORTED (4)
#define CURRENT_VERSION_SUPPORTED (7)

    // The lowest supported version is 4.
    If (pCardData->dwVersion < MINIMUM_VERSION_SUPPORTED)
    {
        dwError = (DWORD) ERROR_REVISION_MISMATCH;
        goto Ret;
    }

    // Set the version to what we support, but don’t exceed the
    // requested version
    pCardData->dwVersion =
       min(pCardData->dwVersion, CURRENT_VERSION_SUPPORTED);
```

**注意**   如果卡微型驱动程序返回的版本不适用于调用应用程序的目的，则调用应用程序负责处理此情况。

 

在对[**CardAcquireContext**](/previous-versions/dn468701(v=vs.85))的调用中设置**dwVersion**后，假设调用方或卡片微型驱动程序在同一上下文中时不会对其进行更改。

### <a name="span-idother_structure_version_checksspanspan-idother_structure_version_checksspanspan-idother_structure_version_checksspanother-structure-version-checks"></a><span id="Other_Structure_Version_Checks"></span><span id="other_structure_version_checks"></span><span id="OTHER_STRUCTURE_VERSION_CHECKS"></span>其他结构版本检查

对于其他版本控制结构和其他卡微型驱动程序 API 方法，版本处理与 [**卡 \_ 数据**](/previous-versions/dn468748(v=vs.85)) 结构相同，但有一个例外。 如果使用包含设置为0的 **dwVersion** 成员的结构调用 API 方法，则必须将此值视为 **dwVersion** 值1。

[**CardRSADecrypt**](/previous-versions/dn468737(v=vs.85))和[**CardSignData**](/previous-versions/dn468741(v=vs.85))函数对传入的数据结构的版本号进行特殊处理。

 

