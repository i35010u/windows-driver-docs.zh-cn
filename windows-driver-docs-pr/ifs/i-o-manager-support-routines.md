---
title: I/o 管理器支持例程
description: I/o 管理器支持例程
ms.assetid: f0b0099e-f920-4287-9e5d-e0fd4241f100
ms.date: 09/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6ae25a05b7f0cd0bc537fbd248ba2a34d564612c
ms.sourcegitcommit: c23a403b3ebea05bde96067b678a318ca9b0cabe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955797"
---
# <a name="io-manager-support-routines"></a>I/o 管理器支持例程

内核模式文件系统和文件系统筛选器（微筛选器或旧筛选器）驱动程序可以调用以下系统提供的 i/o 管理器函数和宏。 设备驱动程序无法使用它们。 它们按字母顺序列出。

除了此处列出的例程，文件系统和筛选器驱动程序还可以调用在*ntifs*中声明的[Windows 内核参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_kernel/)部分中描述的任何 Io*Xxx** * 例程。

**头文件：** *ntifs*

**Prefix：Io @_no__t，_ **IsReparseTag** xxx

| 函数或宏 | 描述 |
| ----------------- | ----------- |
| **IoAcquireVpbSpinLock** | 获取卷参数块（VPB）旋转锁。 |
| **IoAttachDeviceToDeviceStackSafe** | 将调用方的设备对象附加到驱动程序堆栈中最顶层的设备对象。 |
| **IoCancelFileOpen** | 文件系统筛选器驱动程序可用于关闭在筛选器驱动程序的设备堆栈中由文件系统驱动程序打开的文件。 |
| **IoCheckDesiredAccess** | 保留供系统使用。 |
| **IoCheckEaBufferValidity** | 检查指定的扩展特性（EA）缓冲区是否有效。 |
| **IoCheckFunctionAccess** | 保留供系统使用。 |
| **IoCheckQuerySetFileInformation** | 保留供系统使用。 |
| **IoCheckQuerySetVolumeInformation** | 保留供系统使用。 |
| **IoCheckQuotaBufferValidity** | 检查指定的配额缓冲区是否有效。 |
| **IoCreateFileEx** | 导致创建新文件或目录，或打开现有文件、设备、目录或卷，并为调用方提供文件对象的句柄。 文件系统筛选器驱动程序（旧筛选器驱动程序）调用此例程。 |
| **IoCreateFileSpecifyDeviceObjectHint** | 由文件系统筛选器驱动程序用来仅将创建请求发送到指定设备对象下的筛选器和文件系统。 |
| **IoCreateStreamFileObject** | 创建新的流文件对象。 |
| **IoCreateStreamFileObjectEx** | 创建新的流文件对象。 |
| **IoCreateStreamFileObjectEx2** | 创建一个新的流文件对象，其中包含针对目标设备对象的 create 选项。 |
| **IoCreateStreamFileObjectLite** | 创建新的流文件对象，但不会将 IRP_MJ_CLEANUP 请求发送到文件系统驱动程序堆栈。 |
| **IoEnumerateDeviceObjectList** | 枚举驱动程序的设备对象列表。 |
| **IoEnumerateRegisteredFiltersList** | 枚举已向系统注册的文件系统筛选器驱动程序。 |
| **IoFastQueryNetworkAttributes** | 保留供系统使用。 |
| **IoGetAttachedDevice** | 返回一个指针，该指针指向与指定设备关联的最高级别的设备对象。 |
| **IoGetBaseFileSystemDeviceObject** | 保留供系统使用。 |
| **IoGetDeviceAttachmentBaseRef** | 返回指向文件系统或设备驱动程序堆栈中最低级别设备对象的指针。 |
| **IoGetDeviceToVerify** | 返回一个指向设备对象的指针，该对象表示一个可移动媒体设备，该设备是给定线程的 i/o 请求的目标。 |
| **IoGetDiskDeviceObject** | 检索指向与给定文件系统卷设备对象相关联的磁盘设备对象的指针。 |
| **IoGetLowerDeviceObject** | 返回指向驱动程序堆栈上下一级设备对象的指针。 |
| **IoGetOplockKeyContext** | 返回文件对象的目标 oplock 项上下文。 |
| **IoGetOplockKeyContextEx** | 返回文件对象的父和目标 oplock 项上下文。 |
| **IoGetRequestorProcess** | 返回最初请求给定 i/o 操作的线程的进程指针。 |
| **IoGetRequestorProcessId** | 返回最初请求给定 i/o 操作的线程的唯一32位进程 ID。 |
| **IoGetRequestorSessionId** | 返回最初请求给定 i/o 操作的进程的会话 ID。 |
| **IoGetTopLevelIrp** | 返回当前线程的 TopLevelIrp 字段的值。 |
| **IoGetTransactionParameterBloc** | 返回事务处理文件操作的事务参数块。 |
| **IoInitializeDriverCreateContext** | 初始化类型为 IO_DRIVER_CREATE_CONTEXT 的调用方分配的变量。 |
| **IoInitializePriorityInfo** | 初始化 IO_PRIORITY_INFO 类型的结构。 |
| **IoIsFileObjectIgnoringSharing** | 确定是否将文件对象设置为忽略文件共享访问检查的选项。 |
| **IoIsFileOpenedExclusively** | 保留供系统使用。 |
| **IoIsFileOriginRemote** | 确定给定的文件对象是否用于远程创建请求。 |
| **IoIsOperationSynchronous** | 确定给定的 IRP 是否表示同步 i/o 请求。 |
| **IoIsSystemThread** | 检查给定线程是否为系统线程。 |
| **IoIsValidNameGraftingBuffer** | 保留供系统使用。 |
| **IoPageRead** | 保留供系统使用。 |
| **IoQueueThreadIrp** | 保留供系统使用。 |
| **IoQueryFileDosDeviceName** | 检索文件的 MS-DOS 设备名称。 |
| **IoQueryFileInformation** | 保留供系统使用。 |
| **IoQueryVolumeInformation** | 保留供系统使用。 |
| **IoRegisterFileSystem** | 将文件系统的控制设备对象添加到全局文件系统队列。 |
| **IoRegisterFsRegistrationChange** | 注册文件系统筛选器驱动程序的通知例程，每当文件系统将自身注册或注销为活动文件系统时都将调用此例程。 |
| **IoRegisterFsRegistrationChangeEx** | 注册文件系统筛选器驱动程序的通知例程，每当文件系统将自身注册或注销为活动文件系统时都将调用此例程。 |
| **IoRegisterFsRegistrationChangeMountAware** | 注册文件系统筛选器驱动程序的通知例程。 只要文件系统将自身注册或注销为活动文件系统，就会调用此通知例程。 |
| **IoReleaseVpbSpinLock** | 释放卷参数块（VPB）旋转锁。 |
| **IoReplaceFileObjectName** | 替换文件对象的名称。 |
| **IoSetDeviceToVerify** | 指定要验证的设备对象。 指定的设备对象表示可移动媒体设备。 |
| **IoSetFileObjectIgnoreSharing** | 设置一个文件对象，以忽略文件共享访问检查。 |
| **IoSetFileOrigin** | 指定给定文件对象是否用于远程创建请求。 |
| **IoSetInformation** | 保留供系统使用。 |
| **IoSetTopLevelIrp** | 设置当前线程的*TopLevelIrp*字段的值。 |
| **IoSynchronousPageWrite** | 保留供系统使用。 |
| **IoThreadToProcess** | 返回一个指针，该指针指向指定线程的进程。 |
| **IoUnregisterFileSystem** | 从全局文件系统队列中删除文件系统的控制设备对象。 |
| **IoUnregisterFsRegistrationChange** | 取消注册文件系统筛选器驱动程序的文件系统注册更改通知例程。 |
| **IoVerifyVolume** | 将卷验证请求发送到给定的可移动介质设备。 |
| **IsReparseTagMicrosoft** | 确定重分析点标记是否指示 Microsoft 重新分析点。 |
| **IsReparseTagNameSurrogate** | 确定标记的关联重新分析点是否为另一个命名实体（如卷装入点）的代理项。 |
| **IsReparseTagValid** | 保留供系统使用。 |
