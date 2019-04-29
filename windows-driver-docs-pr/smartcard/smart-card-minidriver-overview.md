---
title: 智能卡微型驱动器概述
description: 智能卡微型驱动器概述
ms.assetid: B5047C79-F74E-44FA-ADE5-8716ABC9EB79
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2f48eef2d68b5fb6ae801fe8834a2e4e7121aa1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390910"
---
# <a name="smart-card-minidriver-overview"></a>智能卡微型驱动器概述


特定卡微型驱动程序是最低的逻辑接口层在基本 CSP/KSP。 此微型驱动程序可让基本 CSP/KSP 和应用程序通过使用 SCRM 直接与特定类型的卡交互。

卡微型驱动程序是将一组特定的 Api 导出此规范中定义一个 DLL。 每次调用卡微型驱动程序包括一个指向[**卡\_数据**](https://msdn.microsoft.com/library/windows/hardware/dn468748)提供上下文信息的结构。 此上下文信息提供了一些状态信息除了表的函数指针，用于促进较高层和卡微型驱动程序之间的通信。

此上下文结构的详细信息，请参阅[ **CardAcquireContext**](https://msdn.microsoft.com/library/windows/hardware/dn468701)。

## <a name="span-idrelateddocumentspanspan-idrelateddocumentspanspan-idrelateddocumentspanrelated-document"></a><span id="Related_Document"></span><span id="related_document"></span><span id="RELATED_DOCUMENT"></span>相关的文档


*Cardmod.h* C 标头文件提供了与本规范相关的其他信息。 此文件包含 Microsoft 智能卡微型驱动程序 API 指定的函数原型和结构。 此 API 是通过 Microsoft 加密提供程序开发工具包 (CPDK) 可用。

## <a name="span-idgeneraldesignguidelinesspanspan-idgeneraldesignguidelinesspanspan-idgeneraldesignguidelinesspangeneral-design-guidelines"></a><span id="General_Design_Guidelines"></span><span id="general_design_guidelines"></span><span id="GENERAL_DESIGN_GUIDELINES"></span>一般设计准则


-   应为 DLL 分发卡微型驱动程序。
-   每个特定于卡的操作应实现一个单一的原子事务，除外另有说明，否则。
-   应实现一组标准化的宏观级别操作。
-   逻辑卡文件系统对象应映射到其物理位置。
-   基于此新模型的卡应能够动态地扩展存储在卡的任何文件。 为是只读的并且无法遵守此原则的卡，微型驱动程序应遵循只读的卡的此规格中详述的特定的准则。
-   微型驱动程序从 CPDK 导入定义。 微型驱动程序标头文件 (*Cardmod.h*) 包括*Bcrypt.h*实现此目的。 实现必须解决编译微型驱动程序通过 Microsoft Visual Studio 项目设置此依赖项。
-   插件或驱动程序的受保护进程要求

    -   有关 LSA 插件或驱动程序以受保护的进程的形式成功加载，它必须满足以下条件：

        -   签名验证

            o 受保护模式要求所有插件加载到 LSA 都必须使用 Microsoft 签名进行数字签名。 因此，任何无符号整数，或第三方签名的插件将无法加载到 LSA 中。 此类的插件的示例包括智能卡驱动程序、 加密插件、 密码筛选器，等等。

            o LSA 插件的驱动程序 （如智能卡驱动程序） 需要进行数字签名。

            **请注意**   [Windows 硬件兼容性计划](https://msdn.microsoft.com/library/windows/hardware/dn922588.aspx)提供了用于针对 Windows 进行数字签名的驱动程序的唯一方法。 因此务必来指代此信息的网站。

             

    -   遵守 Microsoft 安全开发生命周期 (SDL) 过程指南。

        -   所有插件还都需要遵守的适用部分[Microsoft 安全开发生命周期 (SDL) – 过程指南](https://msdn.microsoft.com/library/windows/desktop/cc307891.aspx)主题。 有关示例，请参阅*无共享区域*附录 G 中的 SDL 过程中所述

        -   即使使用 Microsoft 签名进行正确签名的插件，不符合 SDL 过程可能会导致加载插件失败。

有关 SDL 的信息，请参阅[Microsoft 安全开发生命周期 (SDL) – 过程指南](https://msdn.microsoft.com/library/windows/desktop/cc307891.aspx)...

有关面向开发人员指南的讨论，请参阅[开发人员指南](developer-guidelines.md)

## <a name="span-idtransactionmanagementspanspan-idtransactionmanagementspanspan-idtransactionmanagementspantransaction-management"></a><span id="Transaction_Management"></span><span id="transaction_management"></span><span id="TRANSACTION_MANAGEMENT"></span>事务管理


-   卡微型驱动程序应假定事务将由调用方，如果它使用 SCRM 访问卡。
-   卡微型驱动程序可以假定所有入口都点除外[ **CardDeleteContext** ](https://msdn.microsoft.com/library/windows/hardware/dn468715)了卡事务调用。 在中，这不能假定**CardDeleteContext**因为卡可能已被删除或清除过程的一部分调用。
-   在单个进程中可以存在多个上下文。 调用[ **CardDeleteContext** ](https://msdn.microsoft.com/library/windows/hardware/dn468715)上一个过程应不会在其他上下文的正常运行。
-   处理的身份验证状态也是卡的调用方不卡微型驱动程序的责任。

## <a name="span-idconventionsspanspan-idconventionsspanspan-idconventionsspanconventions"></a><span id="Conventions"></span><span id="conventions"></span><span id="CONVENTIONS"></span>约定


### <a name="span-idstringsunicodeandansispanspan-idstringsunicodeandansispanspan-idstringsunicodeandansispanstrings-unicode-and-ansi"></a><span id="Strings__UNICODE_and_ANSI"></span><span id="strings__unicode_and_ansi"></span><span id="STRINGS__UNICODE_AND_ANSI"></span>字符串：UNICODE 和 ANSI

在应用程序级别中，直接或间接通常遇到字符串作为用户界面的元素。 因此，它们通常必须本地化 （翻译成用户的语言），以便它们可以理解。 出于此原因，大多数应用程序使用的字符串类型是双字节 (即，UNICODE) 以适应不同的字符集。

但是，智能卡操作最少的资源并且具有很少选项上的命名目录、 文件、 用户和等等。 字符串的字符集是单字节 ANSI，它提供字符串数据的更紧凑表示形式。

相应地，字符串缓冲区与卡微型驱动程序都将是单字节 ANSI，并且要求此字符类型之间的转换必须执行外部卡微型驱动程序。

### <a name="span-iderrorhandlingspanspan-iderrorhandlingspanspan-iderrorhandlingspan-error-handling"></a><span id="_Error_Handling"></span><span id="_error_handling"></span><span id="_ERROR_HANDLING"></span> 错误处理

若要确保一致的错误处理，对失败和一致的行为的卡微型驱动程序，响应应遵循以下约定：

-   所有 NULL 和无效的参数，包括错误的标志都返回放弃\_E\_无效\_参数。
-   所有不正确的 PIN 或尝试使用了错误的键返回放弃\_W\_错误\_CHV。
-   如果出现常规故障发生，Api 返回放弃\_E\_意外的。

此外，以下各节所述的函数返回的错误应该来自放弃\_\*类别 (*winerror.h*)。 例如，我们建议你使用放弃\_E\_无效\_而不是错误的参数 (0x80100004)\_无效\_参数 (0x00000057)。

**请注意**  如果文件不能读取来自 I/O 错误导致卡或其他不可恢复的数据问题，该问题无关的卡，该文件实际是否存在然后 Microsoft 建议返回放弃\_E\_COMM\_数据\_丢失。

返回放弃\_E\_文件\_不\_找到因为在这种情况下，一个涵盖性错误代码提供了具有误导性的调试信息。

 

## <a name="span-idauthenticationandauthorizationspanspan-idauthenticationandauthorizationspanspan-idauthenticationandauthorizationspanauthentication-and-authorization"></a><span id="Authentication_and_Authorization"></span><span id="authentication_and_authorization"></span><span id="AUTHENTICATION_AND_AUTHORIZATION"></span>身份验证和授权


从版本 6 开始，微型驱动程序接口扩展将 PIN 输入到仅仅是一个传统的字母数字字符串以外的概念。 有关详细信息，请参阅"机密\_类型 （枚举）"此规范中更高版本。

## <a name="span-idhandlingmemoryallocationsspanspan-idhandlingmemoryallocationsspanspan-idhandlingmemoryallocationsspanhandling-memory-allocations"></a><span id="Handling_Memory_Allocations"></span><span id="handling_memory_allocations"></span><span id="HANDLING_MEMORY_ALLOCATIONS"></span>处理内存分配


此规范中在内部分配的内存缓冲区的所有 API 元素来执行此都操作调用[ **PFN\_CSP\_分配**](https://msdn.microsoft.com/library/windows/hardware/dn468763)。 因此，必须通过调用释放任何此类内存缓冲区[ **PFN\_CSP\_免费**](https://msdn.microsoft.com/library/windows/hardware/dn468767)。

应通过使用的内存卡微型驱动程序执行任何分配[ **PFN\_CSP\_分配**](https://msdn.microsoft.com/library/windows/hardware/dn468763)或者[ **PFN\_CSP\_REALLOC**](https://msdn.microsoft.com/library/windows/hardware/dn468770)。

## <a name="span-idcachingspanspan-idcachingspanspan-idcachingspancaching"></a><span id="Caching"></span><span id="caching"></span><span id="CACHING"></span>缓存


在基本 CSP/KSP 的卡接口层实现数据缓存，以最大程度减少必须写入或读取从智能卡的数据量。 数据缓存也将可用的卡微型驱动程序可以使用通过函数指针[**卡\_数据**](https://msdn.microsoft.com/library/windows/hardware/dn468748)结构和卡微型驱动程序应使用这些指针来增强通过将缓存其存储在卡的内部数据文件的性能。

数据缓存需要写入访问权限要保留缓存新鲜度计数器到卡片的卡片。 微型驱动程序可以控制数据缓存中，如果对卡写入数据并不可行。

有关如何控制数据缓存的详细信息，请参阅 CP 定义\_卡\_缓存\_中的模式属性[ **CardGetProperty** ](https://msdn.microsoft.com/library/windows/hardware/dn468729)本主题后面规范。

## <a name="span-idmandatoryversioncheckingspanspan-idmandatoryversioncheckingspanspan-idmandatoryversioncheckingspanmandatory-version-checking"></a><span id="Mandatory_Version_Checking"></span><span id="mandatory_version_checking"></span><span id="MANDATORY_VERSION_CHECKING"></span>必需版本检查


所有卡微型驱动程序必须都实现版本检查。 版本[**卡\_数据**](https://msdn.microsoft.com/library/windows/hardware/dn468748)结构是调用方想要支持的版本和卡微型驱动程序实际上可以支持的版本之间进行协商。

### <a name="span-idcarddataversionchecksspanspan-idcarddataversionchecksspanspan-idcarddataversionchecksspancarddata-version-checks"></a><span id="CARD_DATA_Version_Checks"></span><span id="card_data_version_checks"></span><span id="CARD_DATA_VERSION_CHECKS"></span>卡\_数据版本检查

定义为卡微型驱动程序上下文结构的最低版本的最低版本 (即[**卡\_数据**](https://msdn.microsoft.com/library/windows/hardware/dn468748)结构) 的支持，并将当前版本定义的级别为设计此卡微型驱动程序并为卡微型驱动程序集结构的所有项保证可成功返回时从有效[ **CardAcquireContext**](https://msdn.microsoft.com/library/windows/hardware/dn468701)。 当前版本必须是大于或等于最小版本且小于或等于卡\_数据\_当前\_版本中定义*Cardmod.h*。

当调用应用程序调用[ **CardAcquireContext**](https://msdn.microsoft.com/library/windows/hardware/dn468701)，它指定要加载的所需的版本。 在中设置此请求的版本**dw 版本**中的成员[**卡\_数据**](https://msdn.microsoft.com/library/windows/hardware/dn468748)结构。

如果请求的版本低于卡微型驱动程序支持，最小版本[ **CardAcquireContext** ](https://msdn.microsoft.com/library/windows/hardware/dn468701)必须返回一个修订版本不匹配错误 （请参阅下面的示例代码）。

如果请求的版本至少为最小版本很大，应设置卡微型驱动程序**dw 版本**成员到最高版本，它可以支持，它是小于或等于请求的版本。

检查版本时，下面的示例代码显示了预期的卡微型驱动程序行为。 这被假定为中的正文**CardAcquireContext**函数。 *pCardData*指向的指针[**卡\_数据**](https://msdn.microsoft.com/library/windows/hardware/dn468748)结构传递给此调用。

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

**请注意**  卡微型驱动程序返回的版本不适合用于调用应用程序的目的，如果它是调用应用程序以适当地处理此的责任。

 

之后**dw 版本**调用中设置[ **CardAcquireContext**](https://msdn.microsoft.com/library/windows/hardware/dn468701)，假定，它将不会更改由调用方或卡微型驱动程序在同一上下文中时.

### <a name="span-idotherstructureversionchecksspanspan-idotherstructureversionchecksspanspan-idotherstructureversionchecksspanother-structure-version-checks"></a><span id="Other_Structure_Version_Checks"></span><span id="other_structure_version_checks"></span><span id="OTHER_STRUCTURE_VERSION_CHECKS"></span>其他结构版本检查

对于其他版本控制结构和其他卡微型驱动程序 API 方法，版本处理的方法是相同[**卡\_数据**](https://msdn.microsoft.com/library/windows/hardware/dn468748)结构，其中的一个例外。 如果使用结构，其中包含调用 API 方法**dw 版本**设置为 0 的成员，这必须被视为**dw 版本**值为 1。

[ **CardRSADecrypt** ](https://msdn.microsoft.com/library/windows/hardware/dn468737)并[ **CardSignData** ](https://msdn.microsoft.com/library/windows/hardware/dn468741)函数具有特殊处理的数据结构的版本号传入。

 

 





