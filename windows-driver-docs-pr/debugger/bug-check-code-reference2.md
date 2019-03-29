---
title: Bug 检查代码参考
description: 本部分包含常见错误检查，其中包括参数传递到蓝色的屏幕，的说明。
ms.assetid: DBA85578-97CF-4BD7-A67D-1C7AD2E9B2BB
ms.date: 02/21/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4e97477c9d3f29db52840f9d6ed849b8f9a3975e
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743446"
---
# <a name="bug-check-code-reference"></a>Bug 检查代码参考

本部分介绍常见的 bug 检查代码，包括显示在蓝色 bug 检查屏幕上，错误代码的参数。 本部分还介绍如何诊断错误导致的错误检查，以及处理错误的可能方法。

> [!NOTE] 
> 本主题面向程序员。 如果你是其系统具有显示一个包含错误检查代码的蓝色屏幕的客户，请参阅[疑难解答蓝屏错误](https://go.microsoft.com/fwlink/p/?linkid=183646)。

如果此引用中未显示特定的错误检查代码，使用[ **！ 分析**](-analyze.md)扩展在 Windows 调试器 (WinDbg) 使用以下语法 （在内核模式下），替换`<code>`与错误检查代码：

`!analyze -show <code>`

输入此命令使 WinDbg，显示有关指定的错误检查代码的信息。 如果您默认的号码基 （基数） 不是 16，前缀`<code>`与**0x**。

下表显示的代码和名称的每个 bug 检查代码。

| 代码       | 名称                                                                                                                                              |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| 0x00000001 | [**APC\_INDEX\_MISMATCH**](bug-check-0x1--apc-index-mismatch.md)                                                                                  |
| 0x00000002 | [**设备\_队列\_不\_忙**](bug-check-0x2--device-queue-not-busy.md)                                                                           |
| 0x00000003 | [**INVALID\_AFFINITY\_SET**](bug-check-0x3--invalid-affinity-set.md)                                                                              |
| 0x00000004 | [**无效\_数据\_访问\_陷阱**](bug-check-0x4--invalid-data-access-trap.md)                                                                     |
| 0x00000005 | [**无效\_进程\_附加\_尝试**](bug-check-0x5--invalid-process-attach-attempt.md)                                                         |
| 0x00000006 | [**无效\_进程\_分离\_尝试**](bug-check-0x6--invalid-process-detach-attempt.md)                                                         |
| 0x00000007 | [**无效\_软件\_中断**](bug-check-0x7--invalid-software-interrupt.md)                                                                  |
| 0x00000008 | [**IRQL\_不\_调度\_级别**](bug-check-0x8--irql-not-dispatch-level.md)                                                                       |
| 0x00000009 | [**IRQL\_NOT\_GREATER\_OR\_EQUAL**](bug-check-0x9--irql-not-greater-or-equal.md)                                                                  |
| 0x0000000A | [**IRQL\_NOT\_LESS\_OR\_EQUAL**](bug-check-0xa--irql-not-less-or-equal.md)                                                                        |
| 0x0000000B | [**否\_异常\_处理\_支持**](bug-check-0xb--no-exception-handling-support.md)                                                           |
| 0x0000000C | [**MAXIMUM\_WAIT\_OBJECTS\_EXCEEDED**](bug-check-0xc--maximum-wait-objects-exceeded.md)                                                           |
| 0x0000000D | [**MUTEX\_级别\_数\_冲突**](bug-check-0xd--mutex-level-number-violation.md)                                                             |
| 0x0000000E | [**否\_用户\_模式\_上下文**](bug-check-0xe--no-user-mode-context.md)                                                                             |
| 0x0000000F | [**旋转\_锁\_ALREADY\_拥有的**](bug-check-0xf--spin-lock-already-owned.md)                                                                       |
| 0x00000010 | [**旋转\_锁\_不\_拥有的**](bug-check-0x10--spin-lock-not-owned.md)                                                                              |
| 0x00000011 | [**THREAD\_NOT\_MUTEX\_OWNER**](bug-check-0x11--thread-not-mutex-owner.md)                                                                        |
| 0x00000012 | [**陷阱\_原因\_未知**](bug-check-0x12--trap-cause-unknown.md)                                                                                 |
| 0x00000013 | [**空\_线程\_获取器\_列表**](bug-check-0x13--empty-thread-reaper-list.md)                                                                    |
| 0x00000014 | [**创建\_删除\_锁\_不\_已锁定**](bug-check-0x14--create-delete-lock-not-locked.md)                                                         |
| 0x00000015 | [**最后一个\_机会\_调用\_FROM\_KMODE**](bug-check-0x15--last-chance-called-from-kmode.md)                                                         |
| 0x00000016 | [**CID\_处理\_创建**](bug-check-0x16--cid-handle-creation.md)                                                                               |
| 0x00000017 | [**CID\_处理\_删除**](bug-check-0x17--cid-handle-deletion.md)                                                                               |
| 0x00000018 | [**引用\_BY\_指针**](bug-check-0x18--reference-by-pointer.md)                                                                             |
| 0x00000019 | [**错误\_池\_标头**](bug-check-0x19--bad-pool-header.md)                                                                                       |
| 0x0000001A | [**内存\_管理**](bug-check-0x1a--memory-management.md)                                                                                    |
| 0x0000001B | [**PFN\_SHARE\_COUNT**](bug-check-0x1b--pfn-share-count.md)                                                                                       |
| 0x0000001C | [**PFN\_REFERENCE\_COUNT**](bug-check-0x1c--pfn-reference-count.md)                                                                               |
| 0x0000001D | [**否\_旋转\_锁\_可用**](bug-check-0x1d--no-spin-lock-available.md)                                                                        |
| 0x0000001E | [**KMODE\_异常\_不\_已处理**](bug-check-0x1e--kmode-exception-not-handled.md)                                                              |
| 0x0000001F | [**SHARED\_RESOURCE\_CONV\_ERROR**](bug-check-0x1f--shared-resource-conv-error.md)                                                                |
| 0x00000020 | [**KERNEL\_APC\_PENDING\_DURING\_EXIT**](bug-check-0x20--kernel-apc-pending-during-exit.md)                                                       |
| 0x00000021 | [**配额\_下溢**](bug-check-0x21--quota-underflow.md)                                                                                        |
| 0x00000022 | [**FILE\_SYSTEM**](bug-check-0x22--file-system.md)                                                                                                |
| 0x00000023 | [**FAT\_FILE\_SYSTEM**](bug-check-0x23--fat-file-system.md)                                                                                       |
| 0x00000024 | [**NTFS\_FILE\_SYSTEM**](bug-check-0x24--ntfs-file-system.md)                                                                                     |
| 0x00000025 | [**NPFS\_FILE\_SYSTEM**](bug-check-0x25--npfs-file-system.md)                                                                                     |
| 0x00000026 | [**CDFS\_FILE\_SYSTEM**](bug-check-0x26--cdfs-file-system.md)                                                                                     |
| 0x00000027 | [**RDR\_FILE\_SYSTEM**](bug-check-0x27--rdr-file-system.md)                                                                                       |
| 0x00000028 | [**损坏\_访问\_令牌**](bug-check-0x28--corrupt-access-token.md)                                                                             |
| 0x00000029 | [**SECURITY\_SYSTEM**](bug-check-0x29--security-system.md)                                                                                        |
| 0x0000002A | [**不一致\_IRP**](bug-check-0x2a--inconsistent-irp.md)                                                                                      |
| 0x0000002B | [**PANIC\_堆栈\_开关**](bug-check-0x2b--panic-stack-switch.md)                                                                                 |
| 0x0000002C | [**PORT\_DRIVER\_INTERNAL**](bug-check-0x2c--port-driver-internal.md)                                                                             |
| 0x0000002D | [**SCSI\_DISK\_DRIVER\_INTERNAL**](bug-check-0x2d--scsi-disk-driver-internal.md)                                                                  |
| 0x0000002E | [**DATA\_BUS\_ERROR**](bug-check-0x2e--data-bus-error.md)                                                                                         |
| 0x0000002F | [**指令\_总线\_错误**](bug-check-0x2f--instruction-bus-error.md)                                                                           |
| 0x00000030 | [**SET\_OF\_INVALID\_CONTEXT**](bug-check-0x30--set-of-invalid-context.md)                                                                        |
| 0x00000031 | [**阶段 0\_初始化\_失败**](bug-check-0x31--phase0-initialization-failed.md)                                                             |
| 0x00000032 | [**阶段 1\_初始化\_失败**](bug-check-0x32--phase1-initialization-failed.md)                                                             |
| 0x00000033 | [**UNEXPECTED\_INITIALIZATION\_CALL**](bug-check-0x33--unexpected-initialization-call.md)                                                         |
| 0x00000034 | [**缓存\_管理器**](bug-check-0x34--cache-manager.md)                                                                                            |
| 0x00000035 | [**否\_更多\_IRP\_堆栈\_位置**](bug-check-0x35--no-more-irp-stack-locations.md)                                                             |
| 0x00000036 | [**DEVICE\_REFERENCE\_COUNT\_NOT\_ZERO**](bug-check-0x36--device-reference-count-not-zero.md)                                                     |
| 0x00000037 | [**FLOPPY\_INTERNAL\_ERROR**](bug-check-0x37--floppy-internal-error.md)                                                                           |
| 0x00000038 | [**SERIAL\_DRIVER\_INTERNAL**](bug-check-0x38--serial-driver-internal.md)                                                                         |
| 0x00000039 | [**SYSTEM\_EXIT\_OWNED\_MUTEX**](bug-check-0x39--system-exit-owned-mutex.md)                                                                      |
| 0x0000003A | [**系统\_展开\_上一步\_用户**](bug-check-0x3a--system-unwind-previous-user.md)                                                              |
| 0x0000003B | [**SYSTEM\_SERVICE\_EXCEPTION**](bug-check-0x3b--system-service-exception.md)                                                                     |
| 0x0000003C | [**中断\_展开\_已尝试**](bug-check-0x3c--interrupt-unwind-attempted.md)                                                                 |
| 0x0000003D | [**中断\_异常\_不\_已处理**](bug-check-0x3d--interrupt-exception-not-handled.md)                                                      |
| 0x0000003E | [**包含多个处理器\_配置\_不\_支持**](bug-check-0x3e--multiprocessor-configuration-not-supported.md)                                |
| 0x0000003F | [**否\_更多\_系统\_PTE**](bug-check-0x3f--no-more-system-ptes.md)                                                                              |
| 0x00000040 | [**目标\_MDL\_过\_小**](bug-check-0x40--target-mdl-too-small.md)                                                                            |
| 0x00000041 | [**必须\_SUCCEED\_池\_空**](bug-check-0x41--must-succeed-pool-empty.md)                                                                      |
| 0x00000042 | [**ATDISK\_DRIVER\_INTERNAL**](bug-check-0x42--atdisk-driver-internal.md)                                                                         |
| 0x00000043 | [**否\_SUCH\_分区**](bug-check-0x43--no-such-partition.md)                                                                                   |
| 0x00000044 | [**多个\_IRP\_完成\_请求**](bug-check-0x44--multiple-irp-complete-requests.md)                                                        |
| 0x00000045 | [**不足\_系统\_映射\_REGS**](bug-check-0x45--insufficient-system-map-regs.md)                                                            |
| 0x00000046 | [**DEREF\_未知\_登录\_会话**](bug-check-0x46--deref-unknown-logon-session.md)                                                              |
| 0x00000047 | [**REF\_未知\_登录\_会话**](bug-check-0x47--ref-unknown-logon-session.md)                                                                  |
| 0x00000048 | [**取消\_状态\_IN\_COMPLETED\_IRP**](bug-check-0x48--cancel-state-in-completed-irp.md)                                                         |
| 0x00000049 | [**页\_容错\_WITH\_中断\_OFF**](bug-check-0x49--page-fault-with-interrupts-off.md)                                                       |
| 0x0000004A | [**IRQL\_GT\_ZERO\_AT\_SYSTEM\_SERVICE**](bug-check-0x4a--irql-gt-zero-at-system-service.md)                                                      |
| 0x0000004B | [**STREAMS\_INTERNAL\_ERROR**](bug-check-0x4b--streams-internal-error.md)                                                                         |
| 0x0000004C | [**FATAL\_UNHANDLED\_HARD\_ERROR**](bug-check-0x4c--fatal-unhandled-hard-error.md)                                                                |
| 0x0000004D | [**否\_页面\_可用**](bug-check-0x4d--no-pages-available.md)                                                                                 |
| 0x0000004E | [**PFN\_列表\_损坏**](bug-check-0x4e--pfn-list-corrupt.md)                                                                                     |
| 0x0000004F | [**NDIS\_INTERNAL\_ERROR**](bug-check-0x4f--ndis-internal-error.md)                                                                               |
| 0x00000050 | [**页\_容错\_IN\_未分页\_区域**](bug-check-0x50--page-fault-in-nonpaged-area.md)                                                             |
| 0x00000051 | [**注册表\_错误**](bug-check-0x51--registry-error.md)                                                                                          |
| 0x00000052 | [**MAILSLOT\_FILE\_SYSTEM**](bug-check-0x52--mailslot-file-system.md)                                                                             |
| 0x00000053 | [**否\_启动\_设备**](bug-check-0x53--no-boot-device.md)                                                                                         |
| 0x00000054 | [**LM\_SERVER\_INTERNAL\_ERROR**](bug-check-0x54--lm-server-internal-error.md)                                                                    |
| 0x00000055 | [**DATA\_COHERENCY\_EXCEPTION**](bug-check-0x55--data-coherency-exception.md)                                                                     |
| 0x00000056 | [**指令\_协调性\_异常**](bug-check-0x56--instruction-coherency-exception.md)                                                       |
| 0x00000057 | [**XNS\_INTERNAL\_ERROR**](bug-check-0x57--xns-internal-error.md)                                                                                 |
| 0x00000058 | [**FTDISK\_INTERNAL\_ERROR**](bug-check-0x58--ftdisk-internal-error.md)                                                                           |
| 0x00000059 | [**PINBALL\_FILE\_SYSTEM**](bug-check-0x59--pinball-file-system.md)                                                                               |
| 0x0000005A | [**关键\_服务\_失败**](bug-check-0x5a--critical-service-failed.md)                                                                       |
| 0x0000005B | [**SET\_ENV\_VAR\_FAILED**](bug-check-0x5b--set-env-var-failed.md)                                                                                |
| 0x0000005C | [**HAL\_初始化\_失败**](bug-check-0x5c--hal-initialization-failed.md)                                                                   |
| 0x0000005D | [**不支持\_处理器**](bug-check-0x5d--unsupported-processor.md)                                                                            |
| 0x0000005E | [**对象\_初始化\_失败**](bug-check-0x5e--object-initialization-failed.md)                                                             |
| 0x0000005F | [**安全\_初始化\_失败**](bug-check-0x5f--security-initialization-failed.md)                                                         |
| 0x00000060 | [**进程\_初始化\_失败**](bug-check-0x60--process-initialization-failed.md)                                                           |
| 0x00000061 | [**HAL1\_初始化\_失败**](bug-check-0x61--hal1-initialization-failed.md)                                                                 |
| 0x00000062 | [**对象 1\_初始化\_失败**](bug-check-0x62--object1-initialization-failed.md)                                                           |
| 0x00000063 | [**SECURITY1\_初始化\_失败**](bug-check-0x63--security1-initialization-failed.md)                                                       |
| 0x00000064 | [**符号\_初始化\_失败**](bug-check-0x64--symbolic-initialization-failed.md)                                                         |
| 0x00000065 | [**MEMORY1\_初始化\_失败**](bug-check-0x65--memory1-initialization-failed.md)                                                           |
| 0x00000066 | [**缓存\_初始化\_失败**](bug-check-0x66--cache-initialization-failed.md)                                                               |
| 0x00000067 | [**CONFIG\_初始化\_失败**](bug-check-0x67--config-initialization-failed.md)                                                             |
| 0x00000068 | [**文件\_初始化\_失败**](bug-check-0x68--file-initialization-failed.md)                                                                 |
| 0x00000069 | [**IO1\_初始化\_失败**](bug-check-0x69--io1-initialization-failed.md)                                                                   |
| 0x0000006A | [**LPC\_初始化\_失败**](bug-check-0x6a--lpc-initialization-failed.md)                                                                   |
| 0x0000006B | [**PROCESS1\_初始化\_失败**](bug-check-0x6b--process1-initialization-failed.md)D                                                         |
| 0x0000006C | [**REFMON\_初始化\_失败**](bug-check-0x6c--refmon-initialization-failed.md)                                                             |
| 0x0000006D | [**SESSION1\_初始化\_失败**](bug-check-0x6d--session1-initialization-failed.md)                                                         |
| 0x0000006E | [**SESSION2\_初始化\_失败**](bug-check-0x6e--session2-initialization-failed.md)                                                         |
| 0x0000006F | [**SESSION3\_初始化\_失败**](bug-check-0x6f--session3-initialization-failed.md)                                                         |
| 0x00000070 | [**SESSION4\_初始化\_失败**](bug-check-0x70--session4-initialization-failed.md)                                                         |
| 0x00000071 | [**SESSION5\_初始化\_失败**](bug-check-0x71--session5-initialization-failed.md)                                                         |
| 0x00000072 | [**ASSIGN\_DRIVE\_LETTERS\_FAILED**](bug-check-0x72--assign-drive-letters-failed.md)                                                              |
| 0x00000073 | [**CONFIG\_列表\_失败**](bug-check-0x73--config-list-failed.md)                                                                                 |
| 0x00000074 | [**错误\_系统\_CONFIG\_信息**](bug-check-0x74--bad-system-config-info.md)                                                                        |
| 0x00000075 | [**不能\_编写\_配置**](bug-check-0x75--cannot-write-configuration.md)                                                                 |
| 0x00000076 | [**进程\_HAS\_已锁定\_页**](bug-check-0x76--process-has-locked-pages.md)                                                                    |
| 0x00000077 | [**KERNEL\_STACK\_INPAGE\_ERROR**](bug-check-0x77--kernel-stack-inpage-error.md)                                                                  |
| 0x00000078 | [**PHASE0\_EXCEPTION**](bug-check-0x78--phase0-exception.md)                                                                                      |
| 0x00000079 | [**不匹配的\_HAL**](bug-check-0x79--mismatched-hal.md)                                                                                          |
| 0x0000007A | [**KERNEL\_DATA\_INPAGE\_ERROR**](bug-check-0x7a--kernel-data-inpage-error.md)                                                                    |
| 0x0000007B | [**无法访问\_启动\_设备**](bug-check-0x7b--inaccessible-boot-device.md)                                                                     |
| 0x0000007C | [**BUGCODE\_NDIS\_驱动程序**](bug-check-0x7c--bugcode-ndis-driver.md)                                                                               |
| 0x0000007D | [**安装\_详细\_内存**](bug-check-0x7d--install-more-memory.md)                                                                               |
| 0x0000007E | [**系统\_线程\_异常\_不\_已处理**](bug-check-0x7e--system-thread-exception-not-handled.md)                                             |
| 0x0000007F | [**UNEXPECTED\_KERNEL\_MODE\_TRAP**](bug-check-0x7f--unexpected-kernel-mode-trap.md)                                                              |
| 0x00000080 | [**NMI\_硬件\_失败**](bug-check-0x80--nmi-hardware-failure.md)                                                                             |
| 0x00000081 | [**旋转\_锁\_INIT\_失败**](bug-check-0x81--spin-lock-init-failure.md)                                                                        |
| 0x00000082 | [**DFS\_FILE\_SYSTEM**](bug-check-0x82--dfs-file-system.md)                                                                                       |
| 0x00000085 | [**安装程序\_失败**](bug-check-0x85--setup-failure.md)                                                                                            |
| 0x0000008B | [**MBR\_校验和\_不匹配**](bug-check-0x8b--mbr-checksum-mismatch.md)                                                                           |
| 0x0000008E | [**KERNEL\_MODE\_EXCEPTION\_NOT\_HANDLED**](bug-check-0x8e--kernel-mode-exception-not-handled.md)                                                 |
| 0x0000008F | [**PP0\_初始化\_失败**](bug-check-0x8f--pp0-initialization-failed.md)                                                                   |
| 0x00000090 | [**PP1\_初始化\_失败**](bug-check-0x90--pp1-initialization-failed.md)                                                                   |
| 0x00000092 | [**UP\_DRIVER\_ON\_MP\_SYSTEM**](bug-check-0x92--up-driver-on-mp-system.md)                                                                       |
| 0x00000093 | [**INVALID\_KERNEL\_HANDLE**](bug-check-0x93--invalid-kernel-handle.md)                                                                           |
| 0x00000094 | [**KERNEL\_STACK\_LOCKED\_AT\_EXIT**](bug-check-0x94--kernel-stack-locked-at-exit.md)                                                             |
| 0x00000096 | [**无效\_工作\_队列\_项**](bug-check-0x96--invalid-work-queue-item.md)                                                                      |
| 0x00000097 | [**绑定\_图像\_不受支持**](bug-check-0x97--bound-image-unsupported.md)                                                                       |
| 0x00000098 | [**结束\_OF\_NT\_评估\_段**](bug-check-0x98--end-of-nt-evaluation-period.md)                                                             |
| 0x00000099 | [**INVALID\_REGION\_OR\_SEGMENT**](bug-check-0x99--invalid-region-or-segment.md)                                                                  |
| 0x0000009A | [**系统\_许可证\_冲突**](bug-check-0x9a--system-license-violation.md)                                                                     |
| 0x0000009B | [**UDFS\_FILE\_SYSTEM**](bug-check-0x9b--udfs-file-system.md)                                                                                     |
| 0x0000009C | [**MACHINE\_CHECK\_EXCEPTION**](bug-check-0x9c--machine-check-exception.md)                                                                       |
| 0x0000009E | [**用户\_模式下\_运行状况\_监视器**](bug-check-0x9e--user-mode-health-monitor.md)                                                                    |
| 0x0000009F | [**DRIVER\_POWER\_STATE\_FAILURE**](bug-check-0x9f--driver-power-state-failure.md)                                                                |
| 0x000000A0 | [**INTERNAL\_POWER\_ERROR**](bug-check-0xa0--internal-power-error.md)                                                                             |
| 0x000000A1 | [**PCI\_BUS\_DRIVER\_INTERNAL**](bug-check-0xa1--pci-bus-driver-internal.md)                                                                      |
| 0x000000A2 | [**内存\_图像\_损坏**](bug-check-0xa2--memory-image-corrupt.md)                                                                             |
| 0x000000A3 | [**ACPI\_DRIVER\_INTERNAL**](bug-check-0xa3--acpi-driver-internal.md)                                                                             |
| 0x000000A4 | [**CNSS\_FILE\_SYSTEM\_FILTER**](bug-check-0xa4--cnss-file-system-filter.md)                                                                      |
| 0x000000A5 | [**ACPI\_BIOS\_ERROR**](bug-check-0xa5--acpi-bios-error.md)                                                                                       |
| 0x000000A7 | [**BAD\_EXHANDLE**](bug-check-0xa7--bad-exhandle.md)                                                                                              |
| 0x000000AB | [**会话\_HAS\_有效\_池\_ON\_退出**](bug-check-0xab--session-has-valid-pool-on-exit.md)                                                      |
| 0x000000AC | [**HAL\_内存\_分配**](bug-check-0xac--hal-memory-allocation.md)                                                                           |
| 0x000000AD | [**视频\_驱动程序\_调试\_报表\_请求**](bug-check-0xad--video-driver-debug-report-request.md)                                                 |
| 0x000000B1 | [**BGI\_检测到\_冲突**](bug-check-0xb1--bgi-detected-violation.md)                                                                         |
| 0x000000B4 | [**视频\_驱动程序\_INIT\_失败**](bug-check-0xb4--video-driver-init-failure.md)                                                                  |
| 0x000000B8 | [**ATTEMPTED\_SWITCH\_FROM\_DPC**](bug-check-0xb8--attempted-switch-from-dpc.md)                                                                  |
| 0x000000B9 | [**CHIPSET\_DETECTED\_ERROR**](bug-check-0xb9--chipset-detected-error.md)                                                                         |
| 0x000000BA | [**会话\_HAS\_有效\_视图\_ON\_退出**](bug-check-0xba--session-has-valid-views-on-exit.md)                                                    |
| 0x000000BB | [**网络\_引导\_初始化\_失败**](bug-check-0xbb--network-boot-initialization-failed.md)                                                |
| 0x000000BC | [**NETWORK\_BOOT\_DUPLICATE\_ADDRESS**](bug-check-0xbc--network-boot-duplicate-address.md)                                                        |
| 0x000000BD | [**INVALID\_HIBERNATED\_STATE**](bug-check-0xbd--invalid-hibernated-state.md)                                                                     |
| 0x000000BE | [**尝试\_编写\_TO\_READONLY\_内存**](bug-check-0xbe--attempted-write-to-readonly-memory.md)                                               |
| 0x000000BF | [**MUTEX\_ALREADY\_拥有的**](bug-check-0xbf--mutex-already-owned.md)                                                                               |
| 0x000000C1 | [**特殊\_池\_已检测\_内存\_损坏**](bug-check-0xc1--special-pool-detected-memory-corruption.md)                                     |
| 0x000000C2 | [**错误\_池\_调用方**](bug-check-0xc2--bad-pool-caller.md)                                                                                       |
| 0x000000C4 | [**DRIVER\_VERIFIER\_DETECTED\_VIOLATION**](bug-check-0xc4--driver-verifier-detected-violation.md)                                                |
| 0x000000C5 | [**驱动程序\_损坏\_EXPOOL**](bug-check-0xc5--driver-corrupted-expool.md)                                                                       |
| 0x000000C6 | [**驱动程序\_CAUGHT\_修改\_FREED\_POO**](bug-check-0xc6--driver-caught-modifying-freed-pool.md)L                                               |
| 0x000000C7 | [**计时器\_或者\_DPC\_无效**](bug-check-0xc7--timer-or-dpc-invalid.md)                                                                            |
| 0x000000C8 | [**IRQL\_UNEXPECTED\_VALUE**](bug-check-0xc8--irql-unexpected-value.md)                                                                           |
| 0x000000C9 | [**DRIVER\_VERIFIER\_IOMANAGER\_VIOLATION**](bug-check-0xc9--driver-verifier-iomanager-violation.md)                                              |
| 0x000000CA | [**PNP\_DETECTED\_FATAL\_ERROR**](bug-check-0xca--pnp-detected-fatal-error.md)                                                                    |
| 0x000000CB | [**驱动程序\_左侧\_已锁定\_页面\_IN\_过程**](bug-check-0xcb--driver-left-locked-pages-in-process.md)                                            |
| 0x000000CC | [**页\_容错\_IN\_FREED\_特殊\_池**](bug-check-0xcc--page-fault-in-freed-special-pool.md)                                                  |
| 0x000000CD | [**页\_容错\_超出\_最终\_OF\_分配**](bug-check-0xcd--page-fault-beyond-end-of-allocation.md)                                            |
| 0x000000CE | [**驱动程序\_UNLOADED\_WITHOUT\_正在取消\_PENDING\_操作**](bug-check-0xce--driver-unloaded-without-cancelling-pending-operations.md)        |
| 0x000000CF | [**终端\_服务器\_驱动程序\_所做\_不正确\_内存\_引用**](bug-check-0xcf--terminal-server-driver-made-incorrect-memory-reference.md)     |
| 0x000000D0 | [**驱动程序\_损坏\_MMPOOL**](bug-check-0xd0--driver-corrupted-mmpool.md)                                                                       |
| 0x000000D1 | [**DRIVER\_IRQL\_NOT\_LESS\_OR\_EQUAL**](bug-check-0xd1--driver-irql-not-less-or-equal.md)                                                        |
| 0x000000D2 | [**BUGCODE\_ID\_驱动程序**](bug-check-0xd2--bugcode-id-driver.md)                                                                                   |
| 0x000000D3 | [**驱动程序\_部分\_必须\_BE\_未分页**](bug-check-0xd3--driver-portion-must-be-nonpaged.md)                                                     |
| 0x000000D4 | [**SYSTEM\_SCAN\_AT\_RAISED\_IRQL\_CAUGHT\_IMPROPER\_DRIVER\_UNLOAD**](bug-check-0xd4--system-scan-at-raised-irql-caught-improper-driver-unlo.md) |
| 0x000000D5 | [**DRIVER\_PAGE\_FAULT\_IN\_FREED\_SPECIAL\_POOL**](bug-check-0xd5--driver-page-fault-in-freed-special-pool.md)                                   |
| 0x000000D6 | [**驱动程序\_页上\_容错\_超出\_最终\_OF\_分配**](bug-check-0xd6--driver-page-fault-beyond-end-of-allocation.md)                             |
| 0x000000D7 | [**驱动程序\_UNMAPPING\_无效\_视图**](bug-check-0xd7--driver-unmapping-invalid-view.md)                                                          |
| 0x000000D8 | [**DRIVER\_USED\_EXCESSIVE\_PTES**](bug-check-0xd8--driver-used-excessive-ptes.md)                                                                |
| 0x000000D9 | [**锁定\_PAGES\_跟踪器\_损坏**](bug-check-0xd9--locked-pages-tracker-corruption.md)                                                      |
| 0x000000DA | [**SYSTEM\_PTE\_MISUSE**](bug-check-0xda--system-pte-misuse.md)                                                                                   |
| 0x000000DB | [**驱动程序\_损坏\_SYSPTES**](bug-check-0xdb--driver-corrupted-sysptes.md)                                                                     |
| 0x000000DC | [**驱动程序\_无效\_堆栈\_访问**](bug-check-0xdc--driver-invalid-stack-access.md)                                                              |
| 0x000000DE | [**池\_损坏\_IN\_文件\_区域**](bug-check-0xde--pool-corruption-in-file-area.md)                                                           |
| 0x000000DF | 我[**模拟\_辅助\_线程**](bug-check-0xdf--impersonating-worker-thread.md)                                                               |
| 0x000000E0 | [**ACPI\_BIOS\_FATAL\_ERROR**](bug-check-0xe0--acpi-bios-fatal-error.md)                                                                          |
| 0x000000E1 | [**WORKER\_THREAD\_RETURNED\_AT\_BAD\_IRQL**](bug-check-0xe1--worker-thread-returned-at-bad-irql.md)                                              |
| 0x000000E2 | [**手动\_启动\_崩溃**](bug-check-0xe2--manually-initiated-crash.md)                                                                     |
| 0x000000E3 | [**资源\_不\_拥有的**](bug-check-0xe3--resource-not-owned.md)                                                                                 |
| 0x000000E4 | [**辅助角色\_无效**](bug-check-0xe4--worker-invalid.md)                                                                                          |
| 0x000000E6 | [**DRIVER\_VERIFIER\_DMA\_VIOLATION**](bug-check-0xe6--driver-verifier-dma-violation.md)                                                          |
| 0x000000E7 | [**无效\_浮动\_点\_状态**](bug-check-0xe7--invalid-floating-point-state.md)                                                            |
| 0x000000E8 | [**INVALID\_CANCEL\_OF\_FILE\_OPEN**](bug-check-0xe8--invalid-cancel-of-file-open.md)                                                             |
| 0x000000E9 | [**ACTIVE\_EX\_辅助角色\_线程\_终止**](bug-check-0xe9--active-ex-worker-thread-termination.md)                                             |
| 0x000000EA | [**THREAD\_STUCK\_IN\_DEVICE\_DRIVER**](bug-check-0xea--thread-stuck-in-device-driver.md)                                                         |
| 0x000000EB | [**脏\_映射\_页面\_拥塞**](bug-check-0xeb--dirty-mapped-pages-congestion.md)                                                          |
| 0x000000EC | [**会话\_HAS\_有效\_特殊\_池\_ON\_退出**](bug-check-0xec--session-has-valid-special-pool-on-exit.md)                                     |
| 0x000000ED | [**之后\_启动\_卷**](bug-check-0xed--unmountable-boot-volume.md)                                                                       |
| 0x000000EF | [**关键\_进程\_DIED**](bug-check-0xef--critical-process-died.md)                                                                           |
| 0x000000F0 | [**存储\_微型端口\_错误**](bug-check-0xf0--storage-miniport-error.md)                                                                         |
| 0x000000F1 | [**SCSI\_VERIFIER\_检测到\_冲突**](bug-check-0xf1--scsi-verifier-detected-violation.md)                                                    |
| 0x000000F2 | [**硬件\_中断\_STORM**](bug-check-0xf2--hardware-interrupt-storm.md)                                                                     |
| 0x000000F3 | [**DISORDERLY\_关闭**](bug-check-0xf3--disorderly-shutdown.md)                                                                                |
| 0x000000F4 | [**关键\_对象\_终止**](bug-check-0xf4--critical-object-termination.md)                                                               |
| 0x000000F5 | [**FLTMGR\_FILE\_SYSTEM**](bug-check-0xf5--fltmgr-file-system.md)                                                                                 |
| 0x000000F6 | [**PCI\_VERIFIER\_检测到\_冲突**](bug-check-0xf6--pci-verifier-detected-violation.md)                                                      |
| 0x000000F7 | [**DRIVER\_OVERRAN\_STACK\_BUFFER**](bug-check-0xf7--driver-overran-stack-buffer.md)                                                              |
| 0x000000F8 | [**RAMDISK\_引导\_初始化\_失败**](bug-check-0xf8--ramdisk-boot-initialization-failed.md)                                                |
| 0x000000F9 | [**驱动程序\_退回\_状态\_重新分析\_有关\_卷\_打开**](bug-check-0xf9--driver-returned-status-reparse-for-volume-open.md)                     |
| 0x000000FA | [**HTTP\_驱动程序\_已损坏**](bug-check-0xfa---http-driver-corrupted.md)                                                                          |
| 0x000000FC | [**尝试\_EXECUTE\_OF\_NOEXECUTE\_内存**](bug-check-0xfc---attempted-execute-of-noexecute-memory.md)                                        |
| 0x000000FD | [**脏\_非写入\_页面\_拥塞**](bug-check-0xfd---dirty-nowrite-pages-congestion.md)                                                       |
| 0x000000FE | [**BUGCODE\_USB\_DRIVER**](bug-check-0xfe--bugcode-usb-driver.md)                                                                                 |
| 0x000000FF | [**RESERVE\_QUEUE\_OVERFLOW**](bug-check-0xff---reserve-queue-overflow.md)                                                                        |
| 0x00000100 | [**加载程序\_阻止\_不匹配**](bug-check-0x100---loader-block-mismatch.md)                                                                         |
| 0x00000101 | [**时钟\_监视器\_超时**](bug-check-0x101---clock-watchdog-timeout.md)                                                                       |
| 0x00000102 | [**DPC\_监视器\_超时**](bug-check-0x102--dpc-watchdog-timeout.md)                                                                            |
| 0x00000103 | [**MUP\_FILE\_SYSTEM**](bug-check-0x103---mup-file-system.md)                                                                                     |
| 0x00000104 | [**AGP\_无效\_访问**](bug-check-0x104---agp-invalid-access.md)                                                                               |
| 0x00000105 | [**AGP\_GART\_损坏**](bug-check-0x105---agp-gart-corruption.md)                                                                             |
| 0x00000106 | [**AGP\_非法\_REPROGRAMMED**](bug-check-0x106---agp-illegally-reprogrammed.md)                                                               |
| 0x00000108 | [**第三个\_参与方\_文件\_系统\_失败**](bug-check-0x108--third-party-file-system-failure.md)                                                    |
| 0x00000109 | [**关键\_结构\_损坏**](bug-check-0x109---critical-structure-corruption.md)                                                         |
| 0x0000010A | [**应用程序\_标记\_初始化\_失败**](bug-check-0x10a---app-tagging-initialization-failed.md)                                                |
| 0x0000010C | [**FSRTL\_EXTRA\_CREATE\_PARAMETER\_VIOLATION**](bug-check-0x10c---fsrtl-extra-create-parameter-violation.md)                                     |
| 0x0000010D | [**WDF\_冲突**](bug-check-0x10d---wdf-violation.md)                                                                                          |
| 0x0000010E | [**视频\_内存\_管理\_内部**](bug-check-0x10e---video-memory-management-internal.md)                                                  |
| 0x0000010F | [**RESOURCE\_MANAGER\_EXCEPTION\_NOT\_HANDLED**](bug-check-0x10f---resource-manager-exception-not-handled.md)                                     |
| 0x00000111 | [**RECURSIVE\_NMI**](bug-check-0x111---recursive-nmi.md)                                                                                          |
| 0x00000112 | [**MSRPC\_状态\_冲突**](bug-check-0x112---msrpc-state-violation.md)                                                                         |
| 0x00000113 | [**VIDEO\_DXGKRNL\_FATAL\_ERROR**](bug-check-0x113---video-dxgkrnl-fatal-error.md)                                                                |
| 0x00000114 | [**VIDEO\_SHADOW\_DRIVER\_FATAL\_ERROR**](bug-check-0x114---video-shadow-driver-fatal-error.md)                                                   |
| 0x00000115 | [**AGP\_INTERNAL**](bug-check-0x115---agp-internal.md)                                                                                            |
| 0x00000116 | [**视频\_TDR\_失败**](bug-check-0x116---video-tdr-failure.md)                                                                                     |
| 0x00000117 | [**VIDEO\_TDR\_TIMEOUT\_DETECTED**](bug-check-0x117---video-tdr-timeout-detected.md)                                                              |
| 0x00000119 | [**VIDEO\_SCHEDULER\_INTERNAL\_ERROR**](bug-check-0x119---video-scheduler-internal-error.md)                                                      |
| 0x0000011A | [**EM\_初始化\_失败**](bug-check-0x11a---em-initialization-failure.md)                                                                 |
| 0x0000011B | [**驱动程序\_退回\_持有\_取消\_锁**](bug-check-0x11b---driver-returned-holding-cancel-lock.md)                                           |
| 0x0000011C | [**尝试\_编写\_TO\_CM\_受保护\_存储**](bug-check-0x11c--attempted-write-to-cm-protected-storage.md)                                   |
| 0x0000011D | [**EVENT\_TRACING\_FATAL\_ERROR**](bug-check-0x11d---event-tracing-fatal-error.md)                                                                |
| 0x0000011E | [**太\_许多\_递归\_错误**](bug-check-0x11e--too-many-recursive-faults.md)                                                                |
| 0x0000011F | [**INVALID\_DRIVER\_HANDLE**](bug-check-0x11f--invalid-driver-handle.md)                                                                         |
| 0x00000120 | [**BITLOCKER\_致命错误\_错误**](bug-check-0x120--bitlocker-fatal-error-.md)                                                                        |
| 0x00000121 | [**驱动程序\_冲突**](bug-check-0x121---driver-violation.md)                                                                                    |
| 0x00000122 | [**WHEA\_INTERNAL\_ERROR**](bug-check-0x122---whea-internal-error.md)                                                                             |
| 0x00000123 | [**CRYPTO\_SELF\_测试\_失败**](bug-check-0x123--crypto-self-test-failure-.md)                                                                 |
| 0x00000124 | [**WHEA\_UNCORRECTABLE\_ERROR**](bug-check-0x124---whea-uncorrectable-error.md)                                                                   |
| 0x00000125 | [**NMR\_无效\_状态**](bug-check-0x125--nmr-invalid-state.md)                                                                                 |
| 0x00000126 | [**NETIO\_无效\_池\_调用方**](bug-check-0x126--netio-invalid-pool-caller.md)                                                                |
| 0x00000127 | [**PAGE\_NOT\_ZERO**](bug-check-0x127---page-not-zero.md)                                                                                         |
| 0x00000128 | [**辅助角色\_线程\_返回\_WITH\_错误\_IO\_优先级**](bug-check-0x128--worker-thread-returned-with-bad-io-priority.md)                          |
| 0x00000129 | [**辅助角色\_线程\_返回\_WITH\_错误\_分页\_IO\_优先级**](bug-check-0x129--worker-thread-returned-with-bad-paging-io-priority.md)           |
| 0x0000012A | [**MUI\_否\_有效\_系统\_语言**](bug-check-0x12a--mui-no-valid-system-language.md)                                                          |
| 0x0000012B | [**发生故障\_硬件\_损坏\_页**](bug-check-0x12b---faulty-hardware-corrupted-page.md)                                                      |
| 0x0000012C | [**EXFAT\_FILE\_SYSTEM**](bug-check-0x12c---exfat-file-system.md)                                                                                 |
| 0x0000012D | [**VOLSNAP\_OVERLAPPED\_TABLE\_ACCESS**](bug-check-0x12d--volsnap-overlapped-table-access.md)                                                     |
| 0x0000012E | [**INVALID\_MDL\_RANGE**](bug-check-0x12e--invalid-mdl-range.md)                                                                                  |
| 0x0000012F | [**VHD\_引导\_初始化\_失败**](bug-check-0x12f--vhd-boot-initialization-failed.md)                                                       |
| 0x00000130 | [**DYNAMIC\_ADD\_PROCESSOR\_MISMATCH**](bug-check-0x130--dynamic-add-processor-mismatch.md)                                                       |
| 0x00000131 | [**无效\_扩展\_处理器\_状态**](bug-check-0x131--invalid-extended-processor-state.md)                                                   |
| 0x00000132 | [**RESOURCE\_OWNER\_POINTER\_INVALID**](bug-check-0x132--resource-owner-pointer-invalid.md)                                                       |
| 0x00000133 | [**DPC\_监视器\_冲突**](bug-check-0x133-dpc-watchdog-violation.md)                                                                         |
| 0x00000134 | [**DRIVE\_EXTENDER**](bug-check-0x134--drive-extender.md)                                                                                         |
| 0x00000135 | [**注册表\_筛选器\_驱动程序\_异常**](bug-check-0x135--registry-filter-driver-exception.md)                                                   |
| 0x00000136 | [**VHD\_引导\_主机\_卷\_不\_ENOUGH\_空间**](bug-check-0x136--vhd-boot-host-volume-not-enough-space.md)                                      |
| 0x00000137 | [**WIN32K\_HANDLE\_MANAGER**](bug-check-0x137--win32k-handle-manager.md)                                                                          |
| 0x00000138 | [**GPIO\_控制器\_驱动程序\_错误**](bug-check-0x138-gpio-controller-driver-error.md)                                                            |
| 0x00000139 | [**内核\_安全\_检查\_失败**](bug-check-0x139--kernel-security-check-failure.md)                                              |
| 0x0000013A | [**内核\_模式下\_堆\_损坏**](bug-check-0x13a--kernel-mode-heap-corruption.md)                                                             |
| 0x0000013B | [**PASSIVE\_INTERRUPT\_ERROR**](bug-check-0x13b--passive-interrupt-error.md)                                                                      |
| 0x0000013C | [**无效\_IO\_BOOST\_状态**](bug-check-0x13c--invalid-io-boost-state.md)                                                                       |
| 0x0000013D | [**关键\_初始化\_失败**](bug-check-0x13d--critical-initialization-failure.md)                                                      |
| 0x00000140 | [**存储\_设备\_到异常情况\_检测到**](bug-check-0x140--storage-device-abnormality-detected.md)                                             |
| 0x00000141 | [**VIDEO\_ENGINE\_TIMEOUT\_DETECTED**](bug-check-0x141---video-engine-timeout-detected.md)                                                        |
| 0x00000142 | [**VIDEO\_TDR\_APPLICATION\_BLOCKED**](bug-check-0x142--video-tdr-application-blocked.md)                                                         |
| 0x00000143 | [**PROCESSOR\_DRIVER\_INTERNAL**](bug-check-0x143--processor-driver-internal.md)                                                                  |
| 0x00000144 | [**BUGCODE\_USB3\_DRIVER**](bug-check-0x144--bugcode-usb3-driver.md)                                                                              |
| 0x00000145 | [**安全\_启动\_冲突**](bug-check-0x145--secure-boot-violation-.md)                                                                         |
| 0x00000147 | [**异常\_重置\_检测到**](bug-check-0x147--abnormal-reset-detected.md)                                                                      |
| 0x00000149 | [**REFS\_FILE\_SYSTEM**](bug-check-0x149--refs-file-system.md)                                                                                    |
| 0x0000014A | [**KERNEL\_WMI\_INTERNAL**](bug-check-0x14a--kernel-wmi-internal.md)                                                                              |
| 0x0000014B | [**SOC\_子系统\_失败**](bug-check-0x14b--soc-subsystem-failure.md)                                                                          |
| 0x0000014C | [**FATAL\_ABNORMAL\_RESET\_ERROR**](bug-check-0x14c--fatal-abnormal-reset-error.md)                                                               |
| 0x0000014D | [**异常\_作用域\_无效**](bug-check-0x14d--exception-scope-invalid.md)                                                                      |
| 0x0000014E | [**SOC\_严重\_设备\_已删除**](bug-check-0x14e--soc-critical-device-removed.md)                                                             |
| 0x0000014F | [**PDC\_监视器\_超时**](bug-check-0x14f--pdc-watchdog-timeout.md)                                                                            |
| 0x00000150 | [**TCPIP\_AOAC\_NIC\_ACTIVE\_REFERENCE\_LEAK**](bug-check-0x150--tcpip-aoac-nic-active-reference-leak.md)                                         |
| 0x00000151 | [**不支持\_指令\_模式**](bug-check-0x151--unsupported-instruction-mode.md)                                                            |
| 0x00000152 | [**无效\_推送\_锁\_标志**](bug-check-0x152--invalid-push-lock-flags.md)                                                                     |
| 0x00000153 | [**内核\_锁\_条目\_已泄漏\_ON\_线程\_终止**](bug-check-0x153--kernel-lock-entry-leaked-on-thread-termination.md)                    |
| 0x00000154 | [**意外\_STORE\_异常**](bug-check-0x154--unexpected-store-exception.md)                                                                |
| 0x00000155 | [**OS\_数据\_篡改**](bug-check-0x155--os-data-tampering.md)                                                                                  |
| 0x00000156 | [**WINSOCK\_已检测\_挂起\_套接字句\_LIVEDUMP**](bug-check-0x156--winsock-detected-hung-closesocket-livedump.md)                              |
| 0x00000157 | [**内核\_线程\_优先级\_FLOOR\_冲突**](bug-check-0x157--kernel-thread-priority-floor-violation.md)                                      |
| 0x00000158 | [**ILLEGAL\_IOMMU\_PAGE\_FAULT**](bug-check-0x158--illegal-iommu-page-fault.md)                                                                   |
| 0x00000159 | [**HAL\_ILLEGAL\_IOMMU\_PAGE\_FAULT**](bug-check-0x159--hal-illegal-iommu-page-fault.md)                                                          |
| 0x0000015A | [**SDBUS\_INTERNAL\_ERROR**](bug-check-0x15a--sdbus-internal-error.md)                                                                            |
| 0x0000015B | [**辅助角色\_线程\_返回\_WITH\_系统\_页\_优先级\_ACTIVE**](bug-check-0x15b--worker-thread-returned-with-system-page-priority-active.md) |
| 0x0000015C | [**PDC\_监视器\_超时\_LIVEDUMP**](bug-check-0x15c--pdc-watchdog-timeout-livedump.md)              
| 0x0000015D | [**SOC\_子系统\_失败\_LIVEDUMP**](bug-check-0x15d-soc-subsystem-failure-livedump.md)              
| 0x0000015E | [**BUGCODE\_NDIS\_驱动程序\_LIVE\_转储**](bug-check-0x15e-bugcode-ndis-driver-live-dump.md)                                                         |
| 0x0000015F | [**连接\_待机\_监视器\_超时\_LIVEDUMP**](bug-check-0x15f--connected-standby-watchdog-timeout-livedump.md)                            |
| 0x00000160 | [**WIN32K\_原子\_检查\_失败**](bug-check-0x160--win32k-atomic-check-failure.md)                                                             |
| 0x00000161 | [**LIVE\_SYSTEM\_DUMP**](bug-check-0x161--live-system-dump.md)                                                                                    |
| 0x00000162 | [**KERNEL\_AUTO\_BOOST\_INVALID\_LOCK\_RELEASE**](bug-check-0x162--kernel-auto-boost-invalid-lock-release.md)                                     |
| 0x00000163 | [**辅助角色\_线程\_测试\_条件**](bug-check-0x162--worker-thread-test-condition.md)                                                           |
| 0x00000164 | [**WIN32K\_严重\_失败**](bug-check-0x164--win32k-critical-failure.md)                                                                      |
| 0x00000165 | [**群集\_CSV\_状态\_IO\_超时\_LIVEDUMP**](bug-check-0x165--cluster-csv-staus-io-timeout-livedump.md)                                      | 
| 0x00000166 | [**群集\_资源\_调用\_超时\_LIVEDUMP**](bug-check-0x166--cluster-resource-call-timeout-livedump.md)                                      |
| 0x00000167 | [**CLUSTER\_CSV\_SNAPSHOT\_DEVICE\_INFO\_TIMEOUT\_LIVEDUMP**](bug-check-0x167--cluster-csv-snapshot-device-info-timeout-livedump.md)              |    
| 0x00000168 | [**群集\_CSV\_状态\_过渡\_超时\_LIVEDUMP**](bug-check-0x168--cluster-csv-state-transition-timeout-livedump.md)                       |   
| 0x00000169 | [**群集\_CSV\_卷\_到达\_LIVEDUMP**](bug-check-0x169--cluster-csv-volume-arival-livedump.md)                                             |      
| 0x0000016A | [**群集\_CSV\_卷\_删除\_LIVEDUMP**](bug-check-0x16a--cluster-csv-volume-removal-livedump.md)                                            |    
| 0x0000016B | [**CLUSTER\_CSV_\_CLUSTER\_WATCHDOG_\LIVEDUMP**](bug-check-0x16b--cluster-csv-cluster-watchdog-livedump.md)                                       |   
| 0x0000016C | [**INVALID\_RUNDOWN\_PROTECTION\_FLAGS**](bug-check-0x16c--invalid-rundown-protection-flags.md)                                                   |
| 0x0000016D | [**INVALID\_SLOT\_ALLOCATOR\_FLAGS**](bug-check-0x16d--invalid-slot-allocator-flags.md)                                                           |
| 0x0000016E | [**ERESOURCE\_无效\_版本**](bug-check-0x16e--eresource-invalid-release.md)                                                                  |
| 0x0000016F | [**CLUSTER\_CSV_\STATE\_TRANSITION\_INTERVAL\_TIMEOUT\_LIVEDUMP**](bug-check-0x16f--cluster-csv-state-transistion-interval-livedump.md)           |
| 0x00000170 | [**CRYPTO\_LIBRARY\_INTERNAL\_ERROR**](bug-check-0x170--crypto-library-internal-error.md)                                                         |
| 0x00000171 | [**群集\_CSV\_CLUSSVC\_断开连接\_监视器**](bug-check-0x171--cluster-csv-clussvc-disconnect-watchdog.md)                                    |
| 0x00000173 | [**COREMSGCALL\_INTERNAL\_ERROR**](bug-check-0x173--coremsgcall-internal-error.md)                                                                |
| 0x00000174 | [**COREMSG\_INTERNAL\_ERROR**](bug-check-0x174--coremsg-internal-error.md)                                                                        |
| 0x00000175 | [**以前\_致命错误\_异常\_重置\_错误**](bug-check-0x175--previous-fatal-abnormal-reset-error.md)                                            |
| 0x00000178 | [**ELAM\_DRIVER\_DETECTED\_FATAL\_ERROR**](bug-check-0x175--elam-driver-detected-fatal-error.md)                                                  |
| 0x00000179 | [**群集\_CLUSPORT\_状态\_IO\_超时\_LIVEDUMP**](bug-check-0x179--cluster-clusport-status-io-timeout-livedump.md)                           |
| 0x0000017B | [**探查器\_配置\_非法**](bug-check-0x17b--profiler-configuration-illegal.md)                                                        | 
| 0x0000017C | [**PDC\_锁\_监视器\_LIVEDUMP**](bug-check-0x17c--pdc-lock-watchdog-livedump.md)                                                               | 
| 0x0000017D | [**PDC\_UNEXPECTED\_REVOCATION\_LIVEDUMP**](bug-check-0x17d-unexpected-revocation-livedump.md)                                                    | 
| 0x0000017E | [**微码\_修订\_不匹配**](bug-check-0x17e--microcode-revision-mismatch.md)                                                              | 
| 0x00000187 | [**视频\_DWMINIT\_超时\_回退\_BDD**](bug-check-0x187--video-dwminit-timeout-fallback-bdd.md)                                              |
| 0x00000188 | [**CLUSTER\_CSVFS\_LIVEDUMP**](bug-check-0x188--cluster-csvfs-livedump.md)                                                                        |
| 0x00000189 | [**错误\_对象\_标头**](bug-check-0x189--bad-object-header.md)                                                                                  |
| 0x0000018B | [**SECURE\_KERNEL\_ERROR**](bug-check-0x18b--secure-kernel-error.md)                                                                              |
| 0x0000018C | [**HYPERGUARD\_冲突**](bug-check-0x18c--hyperguard-violation.md)                                                                              |   
| 0x0000018D | [**安全\_容错\_未处理**](bug-check-0x18d--secure-fault-unhandled.md)                                                                        | 
| 0x0000018E | [**KERNEL\_PARTITION\_REFERENCE\_VIOLATION**](bug-check-0x18e--kernel-partition-reference-violation.md)                                           |
| 0x00000190 | [**WIN32K\_CRITICAL\_FAILURE\_LIVEDUMP**](bug-check-0x190--win32k-critical-failure-livedump.md)                                                   |
| 0x00000191 | [**PF\_检测到\_损坏**](bug-check-0x191--pf-detected-corruption.md)                                                                        |
| 0x00000192 | [**内核\_自动\_BOOST\_锁\_采集\_WITH\_凸起\_IRQL**](bug-check-0x192--kernel-auto-boost-lock-acquisition-with-raised-irql.md)         |
| 0x00000193 | [**VIDEO\_DXGKRNL\_LIVEDUMP**](bug-check-0x192--video-dxgkrnl-livedump.md)                                                                        |
| 0x00000195 | [**SMB\_SERVER\_LIVEDUMP**](bug-check-0x195--smb-server-livedump.md)                                                                              |
| 0x00000196 | [**加载程序\_回滚\_检测到**](bug-check-0x196--loader-rollback-detected.md)                                                                    |
| 0x00000197 | [**WIN32K\_安全\_失败**](bug-check-0x197--win32k-security-failure.md)                                                                      |
| 0x00000198 | [**UFX\_LIVEDUMP**](bug-check-0x198--ufx-livedump.md)                                                                                             |
| 0x00000199 | [**KERNEL\_STORAGE\_SLOT\_IN\_USE**](bug-check-0x199--kernel-storage-slot-in-use.md)                                                              |
| 0x0000019A | [**辅助角色\_线程\_返回\_虽然\_附加\_TO\_接收器**](bug-check-0x19a--worker-thread-returned-while-attached-to-silo.md)                      |
| 0x0000019B | [**TTM\_FATAL\_ERROR**](bug-check-0x19b--ttm-fatal-error.md)                                                                                      |
| 0x0000019C | [**WIN32K\_POWER\_WATCHDOG\_TIMEOUT**](bug-check-0x19c--win32k-power-watchdog-timeout.md)                                                         |
| 0x0000019D | [**CLUSTER\_SVHDX\_LIVEDUMP**](bug-check-0x19d--cluster-svhdx-livedump.md)                                                                        |
| 0x000001A0 | [**TTM\_监视器\_超时**](bug-check-0x1a0--ttm-watchdog-timeout.md)                                                                            |
| 0x000001A3 | [**调用\_HAS\_不\_返回\_监视器\_超时\_LIVEDUMP**](bug-check-0x1a3--call-has-not-returned-watchdog-timeout-livedump.md)                  |
| 0x000001A4 | [**DRIPS\_SW\_HW\_DIVERGENCE\_LIVEDUMP**](bug-check-0x1a4--drips-sw-hw-divergence-livedump.md)                                                    |
| 0x000001A5 | [**USB\_DRIPS\_BLOCKER\_SURPRISE\_REMOVAL\_LIVEDUMP**](bug-check-0x1a5--usb-drips-blocker-surprise-removal-livedump.md)                           |
| 0x000001A6 | [**蓝牙\_错误\_恢复\_LIVEDUMP**](bug-check-0x1a6--bluetooth-error-recovery-livedump.md)                                                 |
| 0x000001A7 | [**SMB\_REDIRECTOR\_LIVEDUMP**]bug-check-0x1A7--smb-redirector-livedump.md)                                                                       |
| 0x000001A8 | [**VIDEO\_DXGKRNL\_BLACK\_SCREEN\_LIVEDUMP**](bug-check-0x1a8--video-dxgkrnl-black-screen-livedump.md)                                            |
| 0x000001B0 | [**VIDEO_MINIPORT_FAILED_LIVEDUMP**](bug-check-0x1b0--video-miniport-failed-livedump.md)                                                          |
| 0x000001C4 | [**驱动程序\_VERIFIER\_已检测\_冲突\_LIVEDUMP**](bug-check-0x1c4--driver-verifier-detected-violation-livedump.md)                            |
| 0x000001C5 | [**IO\_THREADPOOL\_DEADLOCK\_LIVEDUMP**](bug-check-0x1c5--io-threadpool-deadlock-livedump.md)                                                     |
| 0x000001C6 | [**快速\_ERESOURCE\_不满足前提条件\_冲突**](bug-check-0x1c6--fast-eresource-precondition-violation.md)                                         |
| 0x000001C7 | [**应用商店\_数据\_结构\_损坏**](bug-check-0x1c7--store-data-structure-corruption.md)                                                     |
| 0x000001C8 | [**手动\_INITIATED\_电源\_按钮\_保存**](bug-check-0x1c8--manually-initiated-power-button-hold.md)                                          |
| 0x000001C9 | [**用户\_模式下\_运行状况\_监视器\_LIVEDUMP**](bug-check-0x1c9--user-mode-health-monitor-livedump.md)                                                |
| 0x000001CA | [**综合\_监视器\_超时**](bug-check-0x1ca--synthetic-watchdog-timeout.md)                                                                |
| 0x000001CB | [**无效\_接收器\_分离**](bug-check-0x1cb--invalid-silo-detach.md)                                                                              |
| 0x000001CC | [**EXRESOURCE_TIMEOUT_LIVEDUMP**](bug-check-0x1cc--exresource-timeout-livedump.md)                                                                |
| 0x000001CD | [**INVALID\_CALLBACK\_STACK_ADDRESS**](bug-check-0x1cd--invalid-callback-stack-address.md)                                                        |
| 0x000001CE | [**INVALID\_KERNEL\_STACK\_ADDRESS**](bug-check-0x1ce--invalid-kernel-stack-address.md)                                                           |
| 0x000001CF | [**硬件\_监视器\_超时**](bug-check-0x1cf--hardware-watchdog-timeout.md)                                                                  |  
| 0x000001D0 | [**CPI\_FIRMWARE\_WATCHDOG\_TIMEOUT**](bug-check-0x1d0--acpi-firmware-watchdog-timeout.md)                                                        |
| 0x000001D1 | [**遥测\_ASSERT 语句\_LIVEDUMP**](bug-check-0x1d1--telemetry-asserts-livedump.md)                                                                |
| 0x000001D2 | [**辅助角色\_线程\_无效\_状态**](bug-check-0x1d2--worker-thread-invalid-state.md)                                                             |
| 0x000001D3 | [**WFP\_无效\_操作**](bug-check-0x1d3--wfp-invalid-operation.md)                                                                          |
| 0x000001D4 | [**UCMUCSI\_LIVEDUMP**](bug-check-0x1d4--ucmusci-livedump.md)                                                                                     |
| 0x000001D5 | [**DRIVER_PNP_WATCHDOG**](bug-check-0x1d5--driver-pnp-watchdog.md)                                                                                |
| 0x000001D6 | [**辅助角色\_线程\_返回\_WITH\_非\_默认\_工作负荷\_类**](bug-check-0x1d6--worker-thread-returned-with-non-default-workload-class.md)   |
| 0x000001D7 | [**EFS\_FATAL\_ERROR**](bug-check-0x1d7--efs-fatal-error.md)                                                                                      |
| 0x000001D8 | [**UCMUCSI\_失败**](bug-check-0x1d8--ucmucsi-failure.md)                                                                                       |
| 0x000001D9 | [**HAL\_IOMMU\_INTERNAL\_ERROR**](bug-check-0x1d8--ucmucsi-failure.md)                                                                            |
| 0x000001DB | [**IPI\_监视器\_超时**](bug-check-0x1db--ipi-watchdog-timeout.md)                                                                            |
| 0x000001DC | [**DMA_COMMON_BUFFER_VECTOR_ERROR**](bug-check-0x1dc--dma-common-buffer-vector-error.md)                                                          |
| 0x00000356 | [**XBOX\_ERACTRL\_CS\_TIMEOUT**](bug-check-0x356--xbox-eractrl-cs-timeout.md)                                                                     |
| 0x00000BFE | [**业务连续性\_蓝牙\_VERIFIER\_容错**](bug-check-0xbfe--bc-bluetooth-verifier-fault.md)                                                             |
| 0x00000BFF | [**BC\_BTHMINI\_VERIFIER\_FAULT**](bug-check-0xbff--bc-bthmini-verifier-fault.md)                                                                 |
| 0x00020001 | [**虚拟机监控程序\_错误**](bug-check-0x20001--hypervisor-error.md)                                                                                   |
| 0x1000007E | [**系统\_线程\_异常\_不\_HANDLED\_M**](bug-check-0x1000007e--system-thread-exception-not-handled-m.md)                                  |
| 0x1000007F | [**UNEXPECTED\_KERNEL\_MODE\_TRAP\_M**](bug-check-0x1000007f--unexpected-kernel-mode-trap-m.md)                                                   |
| 0x1000008E | [**KERNEL\_MODE\_EXCEPTION\_NOT\_HANDLED\_M**](bug-check-0x1000008e--kernel-mode-exception-not-handled-m.md)                                      |
| 0x100000EA | [**THREAD\_STUCK\_IN\_DEVICE\_DRIVER\_M**](bug-check-0x100000ea--thread-stuck-in-device-driver-m.md)                                              |
| 0x4000008A | [**THREAD\_TERMINATE\_HELD\_MUTEX**](bug-check-0x4000008a--thread-terminate-held-mutex.md)                                                        |
| 0xC0000218 | [**状态\_无法\_负载\_注册表\_文件**](bug-check-0xc0000218--status-cannot-load-registry-file.md)                                             |
| 0xC000021A | [**状态\_系统\_进程\_已终止**](bug-check-0xc000021a--status-system-process-terminated.md)                                              |
| 0xC0000221 | [**STATUS\_IMAGE\_CHECKSUM\_MISMATCH**](bug-check-0xc0000221--status-image-checksum-mismatch.md)                                                  |
| 0xDEADDEAD | [**手动\_启动\_CRASH1**](bug-check-0xdeaddead--manually-initiated-crash1.md)                                                             |

 

 

 





