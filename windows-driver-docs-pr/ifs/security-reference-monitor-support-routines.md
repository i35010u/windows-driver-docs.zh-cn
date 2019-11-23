---
title: 安全参考监视器支持例程
description: 安全参考监视器支持例程
ms.assetid: 56cb152b-7c98-48ed-8fe9-72351588e440
ms.date: 09/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: 269e90618d8943e86bc812c05d1484130c98a5bc
ms.sourcegitcommit: c23a403b3ebea05bde96067b678a318ca9b0cabe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955781"
---
# <a name="security-reference-monitor-support-routines"></a>安全参考监视器支持例程

下表列出了系统提供的安全引用支持例程的子集，这些例程可由内核模式文件系统和微筛选器和旧筛选器驱动程序（而不是设备驱动程序）使用。

除了此处所述的例程，文件系统和筛选器驱动程序还可以调用*ntifs*中声明的内核模式驱动程序体系结构参考部分中所述的任何**Se**_Xxx_例程。

**头文件：** *ntifs*

**前缀： Se**_Xxx_

| 函数或宏 | 描述 |
| ----------------- | ----------- |
| **SeAppendPrivileges** | 在访问状态结构中追加额外的特权集权限。 |
| **SeAuditHardLinkCreation** | 保留供系统使用。 |
| **SeAuditingFileEvents** | 确定当前是否正在审核文件打开事件。 |
| **SeAuditingFileOrGlobalEvents** | 确定当前是否正在审核文件或全局事件。 |
| **SeAuditingHardLinkEvents** | 保留供系统使用。 |
| **SeCaptureSubjectContext** | 捕获调用线程的安全上下文以进行访问验证和审核。 |
| **SeCreateClientSecurity** | 使用调用**SeImpersonateClientEx**所需的信息初始化安全客户端上下文结构。 |
| **SeCreateClientSecurityFromSubjectContext** | 检索安全主体上下文的访问令牌，并使用该结果来使用调用**SeImpersonateClientEx**所需的信息来初始化安全客户端上下文。 |
| **SeDeleteClientSecurity** | 删除客户端安全上下文。 |
| **SeDeleteObjectAuditAlarm** | 为标记为删除的对象生成审核和警报消息。 |
| **SeFilterToken** | 创建一个新的访问令牌，它是现有访问令牌的受限版本。 |
| **SeImpersonateClient** | 已过时。 |
| **SeImpersonateClientEx** | 使线程模拟用户。 |
| **SeLengthSid** | 已过时。 |
| **SeLockSubjectContext** | 锁定捕获的主题上下文的主要和模拟标记。 |
| **SeMarkLogonSessionForTerminationNotification** | 标记登录会话，以便在登录会话终止时调用调用方的注册回调例程。 删除引用登录会话的最后一个令牌后，登录会话将终止。 |
| **SeOpenObjectAuditAlarm** | 尝试打开对象时，生成审核和警报消息。 |
| **SeOpenObjectForDeleteAuditAlarm** | 当尝试打开要删除的对象时，将生成审核和警报消息。 |
| **SePrivilegeCheck** | 确定在使用者的访问令牌中是否启用了一组指定的权限。 |
| **SeQueryAuthenticationIdToken** | 检索访问令牌的身份验证 ID。 |
| **SeQueryInformationToken** | 检索有关访问令牌的指定类型的信息。 调用进程必须具有适当的访问权限才能获取该信息。 |
| **SeQuerySecurityDescriptorInfo** | 检索对象的安全描述符的副本。 |
| **SeQuerySessionIdToken** | 保留供系统使用。 |
| **SeQuerySubjectContextToken** | 检索安全主体上下文的访问令牌。 |
| **SeRegisterLogonSessionTerminatedRoutine** | 注册一个在登录会话终止时要调用的回调例程。 删除引用登录会话的最后一个令牌后，登录会话将终止。 |
| **SeReleaseSubjectContext** | 释放先前调用**SeCaptureSubjectContext**捕获的使用者安全上下文。 |
| **SeSetAccessStateGenericMapping** | 设置 ACCESS_STATE 结构的泛型映射字段。 |
| **SeSetSecurityDescriptorInfo** | 设置对象的安全说明符。 |
| **SeSetSecurityDescriptorInfoEx** | 修改对象的安全描述符，并指定该对象是否支持访问控制项（ACE）的自动继承。 |
| **SeSetSessionIdToken** | 保留供系统使用。 |
| **SeStopImpersonatingClient** | 结束用户的调用线程模拟。 |
| **SeTokenIsAdmin** | 确定令牌是否包含本地管理员组。 |
| **SeTokenIsRestricted** | 确定令牌是否包含限制安全标识符（SID）的列表。 |
| **SeTokenType** | 保留供系统使用。 |
| **SeUnlockSubjectContext** | 解除对**SeLockSubjectContext**的调用锁定的已捕获主题上下文的标记锁定。 |
| **SeUnregisterLogonSessionTerminatedRoutine** | 取消注册先前对**SeRegisterLogonSessionTerminatedRoutine**的调用注册的回调例程。 |
