---
title: 支持微筛选器上下文
description: 筛选器管理器为微筛选器上下文提供支持
keywords:
- 筛选器管理器 WDK 文件系统微筛选器，上下文
- 文件系统微筛选器驱动程序 WDK，上下文
- 微筛选器驱动程序 WDK，上下文
- 上下文 WDK 文件系统微筛选器
ms.date: 01/22/2021
ms.localizationpriority: medium
ms.openlocfilehash: aba49144d8bcd79e12762fdd4e7486ea191a377b
ms.sourcegitcommit: 204ed37ede1cd462ef6f6c9211a223fd304da4a5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2021
ms.locfileid: "99502030"
---
# <a name="supporting-minifilter-contexts"></a>支持微筛选器上下文

筛选器管理器提供支持，使微筛选器驱动程序可以将上下文与对象关联起来，以跨 i/o 操作保留状态。 可以具有上下文的对象包括文件、卷、实例、流、流句柄和事务。 有关微筛选器实现的详细信息，请参阅 [关于微筛选器上下文](managing-contexts-in-a-minifilter-driver.md) 。

第三方文件系统必须使用 [**FSRTL_ADVANCED_FCB_HEADER**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsrtl_advanced_fcb_header) 结构 (而不是 [**FSRTL_COMMON_FCB_HEADER**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsrtl_common_fcb_header) 结构) ，才能与流和流句柄上下文正常配合使用。

上下文可以从分页或非分页池分配，但必须从非分页池分配的卷上下文除外。

释放所有未完成的引用后，上下文会自动释放。 如果微筛选器驱动程序定义 [上下文清理回调例程](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_cleanup_callback)，筛选器管理器将在释放上下文之前调用例程。

筛选器管理器负责在删除关联的对象、分离实例以及卸载微筛选器驱动程序时删除上下文。

页面文件或以下操作中不支持上下文：

- 创建请求的 Preoperation 处理

- 关闭请求的 Postoperation 处理

- 处理 IRP_MJ_NETWORK_QUERY_OPEN 请求

有关使用上下文的微筛选器驱动程序的示例，请参阅 [CTX 示例](https://github.com/microsoft/Windows-driver-samples/tree/master/filesys/miniFilter/ctx) 。

## <a name="filter-manager-support-routines-for-context-management"></a>用于上下文管理的筛选器管理器支持例程

筛选器管理器为 minifilters 提供了许多支持上下文支持例程：

- 创建和注册上下文：

  - [**FltAllocateContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext)
  - [**FltRegisterFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)

- 设置上下文：

  - [**FltSetFileContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetfilecontext)
  - [**FltSetInstanceContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetinstancecontext)
  - [**FltSetStreamContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetstreamcontext)
  - [**FltSetStreamHandleContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetstreamhandlecontext)
  - [**FltSetTransactionContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsettransactioncontext)
  - [**FltSetVolumeContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetvolumecontext)

- 查询上下文：

  - [**FltSupportsStreamContexts**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsupportsstreamcontexts)
  - [**FltSupportsStreamHandleContexts**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsupportsstreamhandlecontexts)

- 获取和引用上下文：

  - [**FltGetContexts**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetcontexts)
  - [**FltGetContextsEx**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetcontextsex)
  - [**FltGetFileContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetfilecontext)
  - [**FltGetInstanceContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetinstancecontext)
  - [**FltGetSectionContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetsectioncontext)
  - [**FltGetStreamContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetstreamcontext)
  - [**FltGetStreamHandleContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetstreamhandlecontext)
  - [**FltGetTransactionContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgettransactioncontext)
  - [**FltGetVolumeContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetvolumecontext)
  - [**FltReferenceContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreferencecontext)

- 发布和删除上下文：

  - [**FltDeleteContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletecontext)
  - [**FltDeleteFileContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletefilecontext)
  - [**FltDeleteInstanceContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeleteinstancecontext)
  - [**FltDeleteStreamContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletestreamcontext)
  - [**FltDeleteStreamHandleContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletestreamhandlecontext)
  - [**FltDeleteTransactionContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletetransactioncontext)
  - [**FltDeleteVolumeContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletevolumecontext)
  - [**FltReleaseContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)
  - [**FltReleaseContexts**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontexts)
  - [**FltReleaseContextsEx**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontextsex)
