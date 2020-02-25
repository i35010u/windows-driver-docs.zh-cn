---
title: Bug 检查代码参考
description: 本部分包含常见错误检查的说明，包括传递到蓝屏的参数。
ms.assetid: DBA85578-97CF-4BD7-A67D-1C7AD2E9B2BB
ms.date: 02/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: 61adb0d567024bae0425a104cef9b1802fd5d3a0
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2020
ms.locfileid: "77528973"
---
# <a name="bug-check-code-reference"></a>Bug 检查代码参考

本部分包含常见 Bug 检查代码的说明，包括在蓝色 Bug 检查屏幕上通过错误代码显示的参数。 本节还介绍如何诊断导致错误检查的错误，以及处理错误的可能方法。

> [!NOTE] 
> 本主题面向程序员。 如果你是其系统显示了带有 bug 检查代码的蓝屏的客户，请参阅[排查蓝屏错误](https://go.microsoft.com/fwlink/p/?linkid=183646)。

如果未在此引用中显示特定 bug 检查代码，请在 Windows 调试器（WinDbg）中使用 " [ **！分析**](-analyze.md)扩展" （在内核模式下），将 `<code>` 替换为 bug 检查代码：

`!analyze -show <code>`

输入此命令会导致 WinDbg 显示有关指定 bug 检查代码的信息。 如果默认数字基数（基数）不是16，则前缀 `<code>` **0x**。

下表显示了每个 bug 检查代码的代码和名称。

| 代码       | 名称                                                                                                                                              |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| 0x00000001 | [**APC\_索引\_不匹配**](bug-check-0x1--apc-index-mismatch.md)                                                                                  |
| 0x00000002 | [**设备\_队列\_不\_忙**](bug-check-0x2--device-queue-not-busy.md)                                                                           |
| 0x00000003 | [**设置\_相关性无效\_** ](bug-check-0x3--invalid-affinity-set.md)                                                                              |
| 0x00000004 | [ **\_数据无效\_访问\_陷阱**](bug-check-0x4--invalid-data-access-trap.md)                                                                     |
| 0x00000005 | [**附加\_尝试\_\_处理无效**](bug-check-0x5--invalid-process-attach-attempt.md)                                                         |
| 0x00000006 | [ **\_尝试\_分离\_进程无效**](bug-check-0x6--invalid-process-detach-attempt.md)                                                         |
| 0x00000007 | [ **\_中断的\_软件无效**](bug-check-0x7--invalid-software-interrupt.md)                                                                  |
| 0x00000008 | [**IRQL\_不\_调度\_级别**](bug-check-0x8--irql-not-dispatch-level.md)                                                                       |
| 0x00000009 | [**IRQL\_\_大于\_或\_相等**](bug-check-0x9--irql-not-greater-or-equal.md)                                                                  |
| 0x0000000A | [**IRQL\_\_或\_相等\_** ](bug-check-0xa--irql-not-less-or-equal.md)                                                                        |
| 0x0000000B | [**无\_异常\_处理\_支持**](bug-check-0xb--no-exception-handling-support.md)                                                           |
| 0x0000000C | [**超出\_等待\_对象\_的最大值**](bug-check-0xc--maximum-wait-objects-exceeded.md)                                                           |
| 0x0000000D | [**互斥\_级别\_冲突\_号**](bug-check-0xd--mutex-level-number-violation.md)                                                             |
| 0x0000000E | [**无\_用户\_模式\_上下文**](bug-check-0xe--no-user-mode-context.md)                                                                             |
| 0x0000000F | [**旋转\_锁定\_已\_拥有**](bug-check-0xf--spin-lock-already-owned.md)                                                                       |
| 0x00000010 | [**旋转\_锁定\_未\_拥有**](bug-check-0x10--spin-lock-not-owned.md)                                                                              |
| 0x00000011 | [**线程\_不\_MUTEX\_所有者**](bug-check-0x11--thread-not-mutex-owner.md)                                                                        |
| 0x00000012 | [**陷阱\_原因\_未知**](bug-check-0x12--trap-cause-unknown.md)                                                                                 |
| 0x00000013 | [**空\_线程\_REAPER\_列表**](bug-check-0x13--empty-thread-reaper-list.md)                                                                    |
| 0x00000014 | [**创建\_删除\_锁定\_未\_锁定**](bug-check-0x14--create-delete-lock-not-locked.md)                                                         |
| 0x00000015 | [**上次\_\_从\_KMODE 调用\_** ](bug-check-0x15--last-chance-called-from-kmode.md)                                                         |
| 0x00000016 | [**CID\_处理\_创建**](bug-check-0x16--cid-handle-creation.md)                                                                               |
| 0x00000017 | [**CID\_处理\_删除**](bug-check-0x17--cid-handle-deletion.md)                                                                               |
| 0x00000018 | [ **\_指针\_引用**](bug-check-0x18--reference-by-pointer.md)                                                                             |
| 0x00000019 | [**错误的\_池\_标头**](bug-check-0x19--bad-pool-header.md)                                                                                       |
| 0x0000001A | [**内存\_管理**](bug-check-0x1a--memory-management.md)                                                                                    |
| 0x0000001B | [**PFN\_共享\_计数**](bug-check-0x1b--pfn-share-count.md)                                                                                       |
| 0x0000001C | [**PFN\_引用\_计数**](bug-check-0x1c--pfn-reference-count.md)                                                                               |
| 0x0000001D | [**无\_自旋\_锁定\_可用**](bug-check-0x1d--no-spin-lock-available.md)                                                                        |
| 0x0000001E | [**未\_处理 KMODE\_异常\_** ](bug-check-0x1e--kmode-exception-not-handled.md)                                                              |
| 0x0000001F | [**共享\_资源\_将\_错误**](bug-check-0x1f--shared-resource-conv-error.md)                                                                |
| 0x00000020 | [ **\_退出期间内核\_APC\_挂起\_** ](bug-check-0x20--kernel-apc-pending-during-exit.md)                                                       |
| 0x00000021 | [**配额\_下溢**](bug-check-0x21--quota-underflow.md)                                                                                        |
| 0x00000022 | [**文件\_系统**](bug-check-0x22--file-system.md)                                                                                                |
| 0x00000023 | [**FAT\_文件\_系统**](bug-check-0x23--fat-file-system.md)                                                                                       |
| 0x00000024 | [**NTFS\_文件\_系统**](bug-check-0x24--ntfs-file-system.md)                                                                                     |
| 0x00000025 | [**NPFS\_文件\_系统**](bug-check-0x25--npfs-file-system.md)                                                                                     |
| 0x00000026 | [**CDFS\_文件\_系统**](bug-check-0x26--cdfs-file-system.md)                                                                                     |
| 0x00000027 | [**RDR\_文件\_系统**](bug-check-0x27--rdr-file-system.md)                                                                                       |
| 0x00000028 | [ **\_访问\_标记损坏**](bug-check-0x28--corrupt-access-token.md)                                                                             |
| 0x00000029 | [**安全\_系统**](bug-check-0x29--security-system.md)                                                                                        |
| 0x0000002A | [ **\_IRP 不一致**](bug-check-0x2a--inconsistent-irp.md)                                                                                      |
| 0x0000002B | [**死\_堆栈\_开关**](bug-check-0x2b--panic-stack-switch.md)                                                                                 |
| 0x0000002C | [**端口\_驱动程序\_内部**](bug-check-0x2c--port-driver-internal.md)                                                                             |
| 0x0000002D | [**SCSI\_磁盘\_驱动程序\_内部**](bug-check-0x2d--scsi-disk-driver-internal.md)                                                                  |
| 0x0000002E | [**数据\_总线\_错误**](bug-check-0x2e--data-bus-error.md)                                                                                         |
| 0x0000002F | [**指令\_总线\_错误**](bug-check-0x2f--instruction-bus-error.md)                                                                           |
| 0x00000030 | [**设置\_无效\_上下文的\_** ](bug-check-0x30--set-of-invalid-context.md)                                                                        |
| 0x00000031 | [**阶段 0\_初始化\_失败**](bug-check-0x31--phase0-initialization-failed.md)                                                             |
| 0x00000032 | [**阶段 1\_初始化\_失败**](bug-check-0x32--phase1-initialization-failed.md)                                                             |
| 0x00000033 | [**意外\_初始化\_调用**](bug-check-0x33--unexpected-initialization-call.md)                                                         |
| 0x00000034 | [**缓存\_管理器**](bug-check-0x34--cache-manager.md)                                                                                            |
| 0x00000035 | [**无\_\_IRP\_堆栈\_位置**](bug-check-0x35--no-more-irp-stack-locations.md)                                                             |
| 0x00000036 | [**设备\_引用\_计数\_不\_零**](bug-check-0x36--device-reference-count-not-zero.md)                                                     |
| 0x00000037 | [**软盘\_内部\_错误**](bug-check-0x37--floppy-internal-error.md)                                                                           |
| 0x00000038 | [**串行\_驱动程序\_内部**](bug-check-0x38--serial-driver-internal.md)                                                                         |
| 0x00000039 | [ **\_拥有\_互斥体的系统\_退出**](bug-check-0x39--system-exit-owned-mutex.md)                                                                      |
| 0x0000003A | [**系统\_展开\_上一个\_用户**](bug-check-0x3a--system-unwind-previous-user.md)                                                              |
| 0x0000003B | [**系统\_服务\_异常**](bug-check-0x3b--system-service-exception.md)                                                                     |
| 0x0000003C | [**中断\_展开\_尝试**](bug-check-0x3c--interrupt-unwind-attempted.md)                                                                 |
| 0x0000003D | [**中断\_异常\_未\_处理**](bug-check-0x3d--interrupt-exception-not-handled.md)                                                      |
| 0x0000003E | [**不\_支持多处理器\_配置\_** ](bug-check-0x3e--multiprocessor-configuration-not-supported.md)                                |
| 0x0000003F | [**无\_\_系统\_PTE**](bug-check-0x3f--no-more-system-ptes.md)                                                                              |
| 0x00000040 | [**目标\_MDL\_太\_小**](bug-check-0x40--target-mdl-too-small.md)                                                                            |
| 0x00000041 | [**必须\_成功\_池\_为空**](bug-check-0x41--must-succeed-pool-empty.md)                                                                      |
| 0x00000042 | [**ATDISK\_驱动程序\_内部**](bug-check-0x42--atdisk-driver-internal.md)                                                                         |
| 0x00000043 | [**无\_此类\_分区**](bug-check-0x43--no-such-partition.md)                                                                                   |
| 0x00000044 | [**多\_IRP\_完成\_请求**](bug-check-0x44--multiple-irp-complete-requests.md)                                                        |
| 0x00000045 | [ **\_系统\_MAP\_REGS**](bug-check-0x45--insufficient-system-map-regs.md)                                                            |
| 0x00000046 | [**DEREF\_未知\_登录\_会话**](bug-check-0x46--deref-unknown-logon-session.md)                                                              |
| 0x00000047 | [**引用\_未知\_登录\_会话**](bug-check-0x47--ref-unknown-logon-session.md)                                                                  |
| 0x00000048 | [**已\_IRP 的\_中取消\_状态\_** ](bug-check-0x48--cancel-state-in-completed-irp.md)                                                         |
| 0x00000049 | [**页\_故障\_，并\_关闭\_中断**](bug-check-0x49--page-fault-with-interrupts-off.md)                                                       |
| 0x0000004A | [**IRQL\_GT\_零\_\_系统\_服务**](bug-check-0x4a--irql-gt-zero-at-system-service.md)                                                      |
| 0x0000004B | [**流\_内部\_错误**](bug-check-0x4b--streams-internal-error.md)                                                                         |
| 0x0000004C | [**严重\_未处理\_硬\_错误**](bug-check-0x4c--fatal-unhandled-hard-error.md)                                                                |
| 0x0000004D | [**没有\_页面\_可用**](bug-check-0x4d--no-pages-available.md)                                                                                 |
| 0x0000004E | [**PFN\_列表\_损坏**](bug-check-0x4e--pfn-list-corrupt.md)                                                                                     |
| 0x0000004F | [**NDIS\_内部\_错误**](bug-check-0x4f--ndis-internal-error.md)                                                                               |
| 0x00000050 | [ **\_非分页\_区域中的页面\_错误\_** ](bug-check-0x50--page-fault-in-nonpaged-area.md)                                                             |
| 0x00000051 | [**注册表\_错误**](bug-check-0x51--registry-error.md)                                                                                          |
| 0x00000052 | [**MAILSLOT\_文件\_系统**](bug-check-0x52--mailslot-file-system.md)                                                                             |
| 0x00000053 | [**无\_启动\_设备**](bug-check-0x53--no-boot-device.md)                                                                                         |
| 0x00000054 | [**LM\_SERVER\_内部\_错误**](bug-check-0x54--lm-server-internal-error.md)                                                                    |
| 0x00000055 | [**数据\_一致性\_异常**](bug-check-0x55--data-coherency-exception.md)                                                                     |
| 0x00000056 | [**指令\_一致性\_异常**](bug-check-0x56--instruction-coherency-exception.md)                                                       |
| 0x00000057 | [**XNS\_内部\_错误**](bug-check-0x57--xns-internal-error.md)                                                                                 |
| 0x00000058 | [**FTDISK\_内部\_错误**](bug-check-0x58--ftdisk-internal-error.md)                                                                           |
| 0x00000059 | [**弹球\_文件\_系统**](bug-check-0x59--pinball-file-system.md)                                                                               |
| 0x0000005A | [**严重\_服务\_失败**](bug-check-0x5a--critical-service-failed.md)                                                                       |
| 0x0000005B | [**设置\_ENV\_VAR\_失败**](bug-check-0x5b--set-env-var-failed.md)                                                                                |
| 0x0000005C | [**HAL\_初始化\_失败**](bug-check-0x5c--hal-initialization-failed.md)                                                                   |
| 0x0000005D | [**不支持的\_处理器**](bug-check-0x5d--unsupported-processor.md)                                                                            |
| 0x0000005E | [**对象\_初始化\_失败**](bug-check-0x5e--object-initialization-failed.md)                                                             |
| 0x0000005F | [**安全\_初始化\_失败**](bug-check-0x5f--security-initialization-failed.md)                                                         |
| 0x00000060 | [**进程\_初始化\_失败**](bug-check-0x60--process-initialization-failed.md)                                                           |
| 0x00000061 | [**HAL1\_初始化\_失败**](bug-check-0x61--hal1-initialization-failed.md)                                                                 |
| 0x00000062 | [**OBJECT1\_初始化\_失败**](bug-check-0x62--object1-initialization-failed.md)                                                           |
| 0x00000063 | [**SECURITY1\_初始化\_失败**](bug-check-0x63--security1-initialization-failed.md)                                                       |
| 0x00000064 | [**符号\_初始化\_失败**](bug-check-0x64--symbolic-initialization-failed.md)                                                         |
| 0x00000065 | [**MEMORY1\_初始化\_失败**](bug-check-0x65--memory1-initialization-failed.md)                                                           |
| 0x00000066 | [**缓存\_初始化\_失败**](bug-check-0x66--cache-initialization-failed.md)                                                               |
| 0x00000067 | [**配置\_初始化\_失败**](bug-check-0x67--config-initialization-failed.md)                                                             |
| 0x00000068 | [**文件\_初始化\_失败**](bug-check-0x68--file-initialization-failed.md)                                                                 |
| 0x00000069 | [**IO1\_初始化\_失败**](bug-check-0x69--io1-initialization-failed.md)                                                                   |
| 0x0000006A | [**LPC\_初始化\_失败**](bug-check-0x6a--lpc-initialization-failed.md)                                                                   |
| 0x0000006B | [**PROCESS1\_次数\_初始化**](bug-check-0x6b--process1-initialization-failed.md)2-d                                                         |
| 0x0000006C | [**REFMON\_初始化\_失败**](bug-check-0x6c--refmon-initialization-failed.md)                                                             |
| 0x0000006D | [**SESSION1\_初始化\_失败**](bug-check-0x6d--session1-initialization-failed.md)                                                         |
| 0x0000006E | [**SESSION2\_初始化\_失败**](bug-check-0x6e--session2-initialization-failed.md)                                                         |
| 0x0000006F | [**SESSION3\_初始化\_失败**](bug-check-0x6f--session3-initialization-failed.md)                                                         |
| 0x00000070 | [**SESSION4\_初始化\_失败**](bug-check-0x70--session4-initialization-failed.md)                                                         |
| 0x00000071 | [**SESSION5\_初始化\_失败**](bug-check-0x71--session5-initialization-failed.md)                                                         |
| 0x00000072 | [**将\_驱动器\_号分配\_失败**](bug-check-0x72--assign-drive-letters-failed.md)                                                              |
| 0x00000073 | [**配置\_列表\_失败**](bug-check-0x73--config-list-failed.md)                                                                                 |
| 0x00000074 | [**错误的\_系统\_CONFIG\_信息**](bug-check-0x74--bad-system-config-info.md)                                                                        |
| 0x00000075 | [**无法\_写入\_配置**](bug-check-0x75--cannot-write-configuration.md)                                                                 |
| 0x00000076 | [**处理\_\_锁定\_页**](bug-check-0x76--process-has-locked-pages.md)                                                                    |
| 0x00000077 | [**内核\_堆栈\_INPAGE\_错误**](bug-check-0x77--kernel-stack-inpage-error.md)                                                                  |
| 0x00000078 | [**阶段 0\_异常**](bug-check-0x78--phase0-exception.md)                                                                                      |
| 0x00000079 | [**不匹配的\_HAL**](bug-check-0x79--mismatched-hal.md)                                                                                          |
| 0x0000007A | [**内核\_数据\_INPAGE\_错误**](bug-check-0x7a--kernel-data-inpage-error.md)                                                                    |
| 0x0000007B | [ **\_BOOT\_设备无法访问**](bug-check-0x7b--inaccessible-boot-device.md)                                                                     |
| 0x0000007C | [**BUGCODE\_NDIS\_驱动程序**](bug-check-0x7c--bugcode-ndis-driver.md)                                                                               |
| 0x0000007D | [**安装\_更多\_内存**](bug-check-0x7d--install-more-memory.md)                                                                               |
| 0x0000007E | [**系统\_线程\_异常\_未\_处理**](bug-check-0x7e--system-thread-exception-not-handled.md)                                             |
| 0x0000007F | [**意外\_内核\_模式\_陷阱**](bug-check-0x7f--unexpected-kernel-mode-trap.md)                                                              |
| 0x00000080 | [**NMI\_硬件\_故障**](bug-check-0x80--nmi-hardware-failure.md)                                                                             |
| 0x00000081 | [**旋转\_锁定\_初始化\_失败**](bug-check-0x81--spin-lock-init-failure.md)                                                                        |
| 0x00000082 | [**DFS\_文件\_系统**](bug-check-0x82--dfs-file-system.md)                                                                                       |
| 0x00000085 | [**安装程序\_失败**](bug-check-0x85--setup-failure.md)                                                                                            |
| 0x0000008B | [**MBR\_校验和\_不匹配**](bug-check-0x8b--mbr-checksum-mismatch.md)                                                                           |
| 0x0000008E | [**内核\_模式\_异常\_未\_处理**](bug-check-0x8e--kernel-mode-exception-not-handled.md)                                                 |
| 0x0000008F | [**PP0\_初始化\_失败**](bug-check-0x8f--pp0-initialization-failed.md)                                                                   |
| 0x00000090 | [**PP1\_初始化\_失败**](bug-check-0x90--pp1-initialization-failed.md)                                                                   |
| 0x00000092 | [ **\_MP\_系统上的\_驱动程序\_** ](bug-check-0x92--up-driver-on-mp-system.md)                                                                       |
| 0x00000093 | [ **\_内核\_句柄无效**](bug-check-0x93--invalid-kernel-handle.md)                                                                           |
| 0x00000094 | [**内核\_堆栈\_锁定\_\_退出**](bug-check-0x94--kernel-stack-locked-at-exit.md)                                                             |
| 0x00000096 | [ **\_工作\_队列\_项无效**](bug-check-0x96--invalid-work-queue-item.md)                                                                      |
| 0x00000097 | [ **\_不支持绑定\_图像**](bug-check-0x97--bound-image-unsupported.md)                                                                       |
| 0x00000098 | [ **\_NT\_评估\_期间的结束\_** ](bug-check-0x98--end-of-nt-evaluation-period.md)                                                             |
| 0x00000099 | [ **\_区域无效\_或\_段**](bug-check-0x99--invalid-region-or-segment.md)                                                                  |
| 0x0000009A | [**系统\_许可证\_冲突**](bug-check-0x9a--system-license-violation.md)                                                                     |
| 0x0000009B | [**UDF\_文件\_系统**](bug-check-0x9b--udfs-file-system.md)                                                                                     |
| 0x0000009C | [**计算机\_检查\_异常**](bug-check-0x9c--machine-check-exception.md)                                                                       |
| 0x0000009E | [**用户\_模式\_运行状况\_监视器**](bug-check-0x9e--user-mode-health-monitor.md)                                                                    |
| 0x0000009F | [**驱动程序\_电源\_状态\_故障**](bug-check-0x9f--driver-power-state-failure.md)                                                                |
| 0x000000A0 | [**内部\_POWER\_错误**](bug-check-0xa0--internal-power-error.md)                                                                             |
| 0x000000A1 | [**PCI\_总线\_驱动程序\_内部**](bug-check-0xa1--pci-bus-driver-internal.md)                                                                      |
| 0x000000A2 | [**内存\_映像\_损坏**](bug-check-0xa2--memory-image-corrupt.md)                                                                             |
| 0x000000A3 | [**ACPI\_驱动程序\_内部**](bug-check-0xa3--acpi-driver-internal.md)                                                                             |
| 0x000000A4 | [**CNSS\_文件\_SYSTEM\_筛选器**](bug-check-0xa4--cnss-file-system-filter.md)                                                                      |
| 0x000000A5 | [**ACPI\_BIOS\_错误**](bug-check-0xa5--acpi-bios-error.md)                                                                                       |
| 0x000000A7 | [**错误的\_EXHANDLE**](bug-check-0xa7--bad-exhandle.md)                                                                                              |
| 0x000000AB | [**会话\_\_有效的\_池\_在\_退出**](bug-check-0xab--session-has-valid-pool-on-exit.md)                                                      |
| 0x000000AC | [**HAL\_内存\_分配**](bug-check-0xac--hal-memory-allocation.md)                                                                           |
| 0x000000AD | [**视频\_驱动程序\_调试\_报表\_请求**](bug-check-0xad--video-driver-debug-report-request.md)                                                 |
| 0x000000B1 | [**检测到\_冲突的 BGI\_** ](bug-check-0xb1--bgi-detected-violation.md)                                                                         |
| 0x000000B4 | [**视频\_驱动程序\_INIT\_故障**](bug-check-0xb4--video-driver-init-failure.md)                                                                  |
| 0x000000B8 | [**尝试从\_DPC\_交换机\_** ](bug-check-0xb8--attempted-switch-from-dpc.md)                                                                  |
| 0x000000B9 | [**检测到\_错误的芯片组\_** ](bug-check-0xb9--chipset-detected-error.md)                                                                         |
| 0x000000BA | [**会话\_在\_退出时\_有效的\_视图\_** ](bug-check-0xba--session-has-valid-views-on-exit.md)                                                    |
| 0x000000BB | [**网络\_启动\_初始化\_失败**](bug-check-0xbb--network-boot-initialization-failed.md)                                                |
| 0x000000BC | [**网络\_启动\_重复\_地址**](bug-check-0xbc--network-boot-duplicate-address.md)                                                        |
| 0x000000BD | [ **\_休眠\_状态无效**](bug-check-0xbd--invalid-hibernated-state.md)                                                                     |
| 0x000000BE | [**尝试\_写入\_到\_READONLY\_内存**](bug-check-0xbe--attempted-write-to-readonly-memory.md)                                               |
| 0x000000BF | [**已\_拥有互斥\_** ](bug-check-0xbf--mutex-already-owned.md)                                                                               |
| 0x000000C1 | [**检测到\_\_的特殊池\_内存\_损坏**](bug-check-0xc1--special-pool-detected-memory-corruption.md)                                     |
| 0x000000C2 | [**错误的\_池\_调用方**](bug-check-0xc2--bad-pool-caller.md)                                                                                       |
| 0x000000C4 | [**检测到\_冲突的驱动程序\_验证程序\_** ](bug-check-0xc4--driver-verifier-detected-violation.md)                                                |
| 0x000000C5 | [**驱动程序\_损坏\_EXPOOL**](bug-check-0xc5--driver-corrupted-expool.md)                                                                       |
| 0x000000C6 | [ **\_修改\_释放\_便便捕获驱动程序\_** ](bug-check-0xc6--driver-caught-modifying-freed-pool.md)L                                               |
| 0x000000C7 | [**计时器\_或\_DPC\_无效**](bug-check-0xc7--timer-or-dpc-invalid.md)                                                                            |
| 0x000000C8 | [**IRQL\_意外的\_值**](bug-check-0xc8--irql-unexpected-value.md)                                                                           |
| 0x000000C9 | [**驱动程序\_验证程序\_IOMANAGER\_冲突**](bug-check-0xc9--driver-verifier-iomanager-violation.md)                                              |
| 0x000000CA | [ **\_严重\_错误检测到 PNP\_** ](bug-check-0xca--pnp-detected-fatal-error.md)                                                                    |
| 0x000000CB | [**在\_进程中，驱动程序\_保留\_锁定\_页\_** ](bug-check-0xcb--driver-left-locked-pages-in-process.md)                                            |
| 0x000000CC | [ **\_释放\_特殊\_池的页面\_错误\_** ](bug-check-0xcc--page-fault-in-freed-special-pool.md)                                                  |
| 0x000000CD | [**页面\_错误\_超出\_分配\_结束\_** ](bug-check-0xcd--page-fault-beyond-end-of-allocation.md)                                            |
| 0x000000CE | [ **\_卸载的驱动程序\_未\_取消\_挂起的操作\_** ](bug-check-0xce--driver-unloaded-without-cancelling-pending-operations.md)        |
| 0x000000CF | [**终端\_SERVER\_驱动程序\_创建\_错误\_内存\_引用**](bug-check-0xcf--terminal-server-driver-made-incorrect-memory-reference.md)     |
| 0x000000D0 | [**驱动程序\_损坏\_MMPOOL**](bug-check-0xd0--driver-corrupted-mmpool.md)                                                                       |
| 0x000000D1 | [**驱动程序\_IRQL\_不\_更少\_或\_相等**](bug-check-0xd1--driver-irql-not-less-or-equal.md)                                                        |
| 0x000000D2 | [**BUGCODE\_ID\_驱动程序**](bug-check-0xd2--bugcode-id-driver.md)                                                                                   |
| 0x000000D3 | [**必须\_\_非分页的驱动程序\_部分\_** ](bug-check-0xd3--driver-portion-must-be-nonpaged.md)                                                     |
| 0x000000D4 | [**系统\_扫描\_在\_引发\_IRQL\_\_不正确的\_驱动程序卸载**](bug-check-0xd4--system-scan-at-raised-irql-caught-improper-driver-unlo.md)\_ |
| 0x000000D5 | [**驱动程序\_页面\_错误\_\_释放\_特殊\_池**](bug-check-0xd5--driver-page-fault-in-freed-special-pool.md)                                   |
| 0x000000D6 | [**驱动\_页面\_错误\_超过\_分配\_结束\_** ](bug-check-0xd6--driver-page-fault-beyond-end-of-allocation.md)                             |
| 0x000000D7 | [**驱动程序\_取消映射\_无效的\_视图**](bug-check-0xd7--driver-unmapping-invalid-view.md)                                                          |
| 0x000000D8 | [ **\_使用的驱动程序\_过多\_PTE**](bug-check-0xd8--driver-used-excessive-ptes.md)                                                                |
| 0x000000D9 | [**锁定\_页面\_跟踪器\_损坏**](bug-check-0xd9--locked-pages-tracker-corruption.md)                                                      |
| 0x000000DA | [**系统\_PTE\_误用**](bug-check-0xda--system-pte-misuse.md)                                                                                   |
| 0x000000DB | [**驱动程序\_损坏\_SYSPTES**](bug-check-0xdb--driver-corrupted-sysptes.md)                                                                     |
| 0x000000DC | [**驱动程序\_\_堆栈\_访问无效**](bug-check-0xdc--driver-invalid-stack-access.md)                                                              |
| 0x000000DE | [ **\_文件\_区域中的池\_损坏\_** ](bug-check-0xde--pool-corruption-in-file-area.md)                                                           |
| 0x000000DF | 我[**模拟\_WORKER\_线程**](bug-check-0xdf--impersonating-worker-thread.md)                                                               |
| 0x000000E0 | [**ACPI\_BIOS\_严重\_错误**](bug-check-0xe0--acpi-bios-fatal-error.md)                                                                          |
| 0x000000E1 | [**辅助\_线程\_返回\_，\_错误\_IRQL**](bug-check-0xe1--worker-thread-returned-at-bad-irql.md)                                              |
| 0x000000E2 | [**手动\_启动\_崩溃**](bug-check-0xe2--manually-initiated-crash.md)                                                                     |
| 0x000000E3 | [**资源\_不\_拥有**](bug-check-0xe3--resource-not-owned.md)                                                                                 |
| 0x000000E4 | [**工作\_无效**](bug-check-0xe4--worker-invalid.md)                                                                                          |
| 0x000000E6 | [**驱动程序\_验证程序\_DMA\_冲突**](bug-check-0xe6--driver-verifier-dma-violation.md)                                                          |
| 0x000000E7 | [ **\_浮点\_点\_状态无效**](bug-check-0xe7--invalid-floating-point-state.md)                                                            |
| 0x000000E8 | [**无效的\_取消\_文件\_\_打开**](bug-check-0xe8--invalid-cancel-of-file-open.md)                                                             |
| 0x000000E9 | [**ACTIVE\_EX\_WORKER\_线程\_终止**](bug-check-0xe9--active-ex-worker-thread-termination.md)                                             |
| 0x000000EA | [ **\_设备\_驱动程序中的线程\_停滞\_** ](bug-check-0xea--thread-stuck-in-device-driver.md)                                                         |
| 0x000000EB | [**脏\_映射\_页面\_拥塞**](bug-check-0xeb--dirty-mapped-pages-congestion.md)                                                          |
| 0x000000EC | [**会话\_\_在\_退出时有效\_特殊\_池\_** ](bug-check-0xec--session-has-valid-special-pool-on-exit.md)                                     |
| 0x000000ED | [ **\_卷无法启动\_启动**](bug-check-0xed--unmountable-boot-volume.md)                                                                       |
| 0x000000EF | [**严重\_进程\_终止**](bug-check-0xef--critical-process-died.md)                                                                           |
| 0x000000F0 | [**存储\_微型端口\_错误**](bug-check-0xf0--storage-miniport-error.md)                                                                         |
| 0x000000F1 | [**检测到\_冲突的 SCSI\_验证程序\_** ](bug-check-0xf1--scsi-verifier-detected-violation.md)                                                    |
| 0x000000F2 | [**硬件\_中断\_风暴**](bug-check-0xf2--hardware-interrupt-storm.md)                                                                     |
| 0x000000F3 | [**DISORDERLY\_关闭**](bug-check-0xf3--disorderly-shutdown.md)                                                                                |
| 0x000000F4 | [ **\_终止的关键\_对象**](bug-check-0xf4--critical-object-termination.md)                                                               |
| 0x000000F5 | [**FLTMGR\_文件\_系统**](bug-check-0xf5--fltmgr-file-system.md)                                                                                 |
| 0x000000F6 | [**检测到的 PCI\_验证程序\_\_冲突**](bug-check-0xf6--pci-verifier-detected-violation.md)                                                      |
| 0x000000F7 | [**驱动程序\_OVERRAN\_堆栈\_缓冲区**](bug-check-0xf7--driver-overran-stack-buffer.md)                                                              |
| 0x000000F8 | [**RAMDISK\_启动\_初始化\_失败**](bug-check-0xf8--ramdisk-boot-initialization-failed.md)                                                |
| 0x000000F9 | [**驱动程序\_\_状态返回\_重新分析\_\_卷\_打开**](bug-check-0xf9--driver-returned-status-reparse-for-volume-open.md)                     |
| 0x000000FA | [**HTTP\_驱动程序\_损坏**](bug-check-0xfa---http-driver-corrupted.md)                                                                          |
| 0x000000FC | [**尝试\_执行\_\_NOEXECUTE\_内存**](bug-check-0xfc---attempted-execute-of-noexecute-memory.md)                                        |
| 0x000000FD | [**脏\_NOWRITE\_页\_拥塞**](bug-check-0xfd---dirty-nowrite-pages-congestion.md)                                                       |
| 0x000000FE | [**BUGCODE\_USB\_驱动程序**](bug-check-0xfe--bugcode-usb-driver.md)                                                                                 |
| 0x000000FF | [**保留\_队列\_溢出**](bug-check-0xff---reserve-queue-overflow.md)                                                                        |
| 0x00000100 | [**加载器\_块\_不匹配**](bug-check-0x100---loader-block-mismatch.md)                                                                         |
| 0x00000101 | [**时钟\_监视器\_超时**](bug-check-0x101---clock-watchdog-timeout.md)                                                                       |
| 0x00000102 | [**DPC\_监视器\_超时**](bug-check-0x102--dpc-watchdog-timeout.md)                                                                            |
| 0x00000103 | [**MUP\_文件\_系统**](bug-check-0x103---mup-file-system.md)                                                                                     |
| 0x00000104 | [**AGP\_无效\_访问**](bug-check-0x104---agp-invalid-access.md)                                                                               |
| 0x00000105 | [**AGP\_GART\_损坏**](bug-check-0x105---agp-gart-corruption.md)                                                                             |
| 0x00000106 | [**AGP\_非法\_REPROGRAMMED**](bug-check-0x106---agp-illegally-reprogrammed.md)                                                               |
| 0x00000108 | [**第三\_方\_文件\_系统\_故障**](bug-check-0x108--third-party-file-system-failure.md)                                                    |
| 0x00000109 | [**严重\_结构\_损坏**](bug-check-0x109---critical-structure-corruption.md)                                                         |
| 0x0000010A | [**应用\_标记\_初始化\_失败**](bug-check-0x10a---app-tagging-initialization-failed.md)                                                |
| 0x0000010C | [**FSRTL\_额外\_CREATE\_参数\_冲突**](bug-check-0x10c---fsrtl-extra-create-parameter-violation.md)                                     |
| 0x0000010D | [**WDF\_冲突**](bug-check-0x10d---wdf-violation.md)                                                                                          |
| 0x0000010E | [ **\_管理\_内部的视频\_内存**](bug-check-0x10e---video-memory-management-internal.md)                                                  |
| 0x0000010F | [**资源\_管理器\_异常\_未\_处理**](bug-check-0x10f---resource-manager-exception-not-handled.md)                                     |
| 0x00000111 | [**RECURSIVE\_NMI**](bug-check-0x111---recursive-nmi.md)                                                                                          |
| 0x00000112 | [**MSRPC\_状态\_冲突**](bug-check-0x112---msrpc-state-violation.md)                                                                         |
| 0x00000113 | [**视频\_DXGKRNL\_严重\_错误**](bug-check-0x113---video-dxgkrnl-fatal-error.md)                                                                |
| 0x00000114 | [**视频\_阴影\_驱动程序\_致命\_错误**](bug-check-0x114---video-shadow-driver-fatal-error.md)                                                   |
| 0x00000115 | [**AGP\_内部**](bug-check-0x115---agp-internal.md)                                                                                            |
| 0x00000116 | [**视频\_TDR\_故障**](bug-check-0x116---video-tdr-failure.md)                                                                                     |
| 0x00000117 | [**检测到视频\_TDR\_超时\_** ](bug-check-0x117---video-tdr-timeout-detected.md)                                                              |
| 0x00000119 | [**视频\_计划程序\_内部\_错误**](bug-check-0x119---video-scheduler-internal-error.md)                                                      |
| 0x0000011A | [**EM\_初始化\_失败**](bug-check-0x11a---em-initialization-failure.md)                                                                 |
| 0x0000011B | [**返回\_驱动程序\_按住\_取消\_锁定**](bug-check-0x11b---driver-returned-holding-cancel-lock.md)                                           |
| 0x0000011C | [**尝试\_写入\_到\_CM\_受保护\_存储中**](bug-check-0x11c--attempted-write-to-cm-protected-storage.md)                                   |
| 0x0000011D | [**事件\_跟踪\_严重\_错误**](bug-check-0x11d---event-tracing-fatal-error.md)                                                                |
| 0x0000011E | [**太\_许多\_递归\_错误**](bug-check-0x11e--too-many-recursive-faults.md)                                                                |
| 0x0000011F | [ **\_驱动程序\_句柄无效**](bug-check-0x11f--invalid-driver-handle.md)                                                                         |
| 0x00000120 | [**BITLOCKER\_严重\_错误**](bug-check-0x120--bitlocker-fatal-error-.md)                                                                        |
| 0x00000121 | [**驱动程序\_冲突**](bug-check-0x121---driver-violation.md)                                                                                    |
| 0x00000122 | [**WHEA\_内部\_错误**](bug-check-0x122---whea-internal-error.md)                                                                             |
| 0x00000123 | [**加密\_自检\_失败\_** ](bug-check-0x123--crypto-self-test-failure-.md)                                                                 |
| 0x00000124 | [**WHEA\_无法纠正\_错误**](bug-check-0x124---whea-uncorrectable-error.md)                                                                   |
| 0x00000125 | [**NMR\_无效\_状态**](bug-check-0x125--nmr-invalid-state.md)                                                                                 |
| 0x00000126 | [**NETIO\_\_池\_调用方无效**](bug-check-0x126--netio-invalid-pool-caller.md)                                                                |
| 0x00000127 | [**页\_不\_零**](bug-check-0x127---page-not-zero.md)                                                                                         |
| 0x00000128 | [**辅助\_线程\_返回\_，\_错误\_IO\_优先级**](bug-check-0x128--worker-thread-returned-with-bad-io-priority.md)                          |
| 0x00000129 | [**辅助\_线程\_返回\_\_错误\_分页\_IO\_优先级**](bug-check-0x129--worker-thread-returned-with-bad-paging-io-priority.md)           |
| 0x0000012A | [**MUI\_\_\_系统\_语言无效**](bug-check-0x12a--mui-no-valid-system-language.md)                                                          |
| 0x0000012B | [**故障\_硬件\_损坏\_页**](bug-check-0x12b---faulty-hardware-corrupted-page.md)                                                      |
| 0x0000012C | [**EXFAT\_文件\_系统**](bug-check-0x12c---exfat-file-system.md)                                                                                 |
| 0x0000012D | [**VOLSNAP\_重叠\_表\_访问**](bug-check-0x12d--volsnap-overlapped-table-access.md)                                                     |
| 0x0000012E | [ **\_MDL\_范围无效**](bug-check-0x12e--invalid-mdl-range.md)                                                                                  |
| 0x0000012F | [**VHD\_启动\_初始化\_失败**](bug-check-0x12f--vhd-boot-initialization-failed.md)                                                       |
| 0x00000130 | [**动态\_添加\_处理器\_不匹配**](bug-check-0x130--dynamic-add-processor-mismatch.md)                                                       |
| 0x00000131 | [ **\_扩展\_处理器\_状态无效**](bug-check-0x131--invalid-extended-processor-state.md)                                                   |
| 0x00000132 | [**资源\_所有者\_指针\_无效**](bug-check-0x132--resource-owner-pointer-invalid.md)                                                       |
| 0x00000133 | [**DPC\_监视器\_冲突**](bug-check-0x133-dpc-watchdog-violation.md)                                                                         |
| 0x00000134 | [**驱动器\_扩展器**](bug-check-0x134--drive-extender.md)                                                                                         |
| 0x00000135 | [**注册表\_筛选器\_驱动程序\_异常**](bug-check-0x135--registry-filter-driver-exception.md)                                                   |
| 0x00000136 | [**VHD\_BOOT\_主机\_卷\_未\_足够\_空间**](bug-check-0x136--vhd-boot-host-volume-not-enough-space.md)                                      |
| 0x00000137 | [**WIN32K.SYS\_处理\_管理器**](bug-check-0x137--win32k-handle-manager.md)                                                                          |
| 0x00000138 | [**GPIO\_控制器\_驱动程序\_错误**](bug-check-0x138-gpio-controller-driver-error.md)                                                            |
| 0x00000139 | [**内核\_安全性\_检查\_故障**](bug-check-0x139--kernel-security-check-failure.md)                                              |
| 0x0000013A | [**内核\_模式\_堆\_损坏**](bug-check-0x13a--kernel-mode-heap-corruption.md)                                                             |
| 0x0000013B | [**被动\_中断\_错误**](bug-check-0x13b--passive-interrupt-error.md)                                                                      |
| 0x0000013C | [ **\_IO\_提升\_状态无效**](bug-check-0x13c--invalid-io-boost-state.md)                                                                       |
| 0x0000013D | [**严重\_初始化\_失败**](bug-check-0x13d--critical-initialization-failure.md)                                                      |
| 0x00000140 | [**检测到存储\_设备\_异常情况\_** ](bug-check-0x140--storage-device-abnormality-detected.md)                                             |
| 0x00000141 | [**检测到视频\_引擎\_超时\_** ](bug-check-0x141---video-engine-timeout-detected.md)                                                        |
| 0x00000142 | [**视频\_TDR\_应用程序\_阻止**](bug-check-0x142--video-tdr-application-blocked.md)                                                         |
| 0x00000143 | [**内部处理器\_驱动程序\_** ](bug-check-0x143--processor-driver-internal.md)                                                                  |
| 0x00000144 | [**BUGCODE\_USB3\_驱动程序**](bug-check-0x144--bugcode-usb3-driver.md)                                                                              |
| 0x00000145 | [**安全\_启动\_冲突**](bug-check-0x145--secure-boot-violation-.md)                                                                         |
| 0x00000147 | [**检测到异常\_重置\_** ](bug-check-0x147--abnormal-reset-detected.md)                                                                      |
| 0x00000149 | [**REFS\_文件\_系统**](bug-check-0x149--refs-file-system.md)                                                                                    |
| 0x0000014A | [**内核\_WMI\_内部**](bug-check-0x14a--kernel-wmi-internal.md)                                                                              |
| 0x0000014B | [**SOC\_子系统\_故障**](bug-check-0x14b--soc-subsystem-failure.md)                                                                          |
| 0x0000014C | [**严重\_异常\_重置\_错误**](bug-check-0x14c--fatal-abnormal-reset-error.md)                                                               |
| 0x0000014D | [**异常\_作用域无效\_** ](bug-check-0x14d--exception-scope-invalid.md)                                                                      |
| 0x0000014E | [**已删除 SOC\_严重\_设备\_** ](bug-check-0x14e--soc-critical-device-removed.md)                                                             |
| 0x0000014F | [**PDC\_监视器\_超时**](bug-check-0x14f--pdc-watchdog-timeout.md)                                                                            |
| 0x00000150 | [**TCPIP\_AOAC\_NIC\_活动\_引用\_泄露**](bug-check-0x150--tcpip-aoac-nic-active-reference-leak.md)                                         |
| 0x00000151 | [**不支持的\_指令\_模式**](bug-check-0x151--unsupported-instruction-mode.md)                                                            |
| 0x00000152 | [ **\_推送\_锁定\_标记无效**](bug-check-0x152--invalid-push-lock-flags.md)                                                                     |
| 0x00000153 | [**内核\_锁定\_条目\_在\_上泄露\_\_终止**](bug-check-0x153--kernel-lock-entry-leaked-on-thread-termination.md)                    |
| 0x00000154 | [**意外的\_存储\_异常**](bug-check-0x154--unexpected-store-exception.md)                                                                |
| 0x00000155 | [**操作系统\_数据\_篡改**](bug-check-0x155--os-data-tampering.md)                                                                                  |
| 0x00000156 | [**WINSOCK\_检测到\_挂起\_导致\_LIVEDUMP**](bug-check-0x156--winsock-detected-hung-closesocket-livedump.md)                              |
| 0x00000157 | [**内核\_线程\_优先级\_底层\_冲突**](bug-check-0x157--kernel-thread-priority-floor-violation.md)                                      |
| 0x00000158 | [**非法\_IOMMU\_页面\_错误**](bug-check-0x158--illegal-iommu-page-fault.md)                                                                   |
| 0x00000159 | [**HAL\_非法\_IOMMU\_页\_错误**](bug-check-0x159--hal-illegal-iommu-page-fault.md)                                                          |
| 0x0000015A | [**SDBUS\_内部\_错误**](bug-check-0x15a--sdbus-internal-error.md)                                                                            |
| 0x0000015B | [**辅助\_线程\_返回\_，\_系统\_的优先级\_** ](bug-check-0x15b--worker-thread-returned-with-system-page-priority-active.md)\_ |
| 0x0000015C | [**PDC\_监视器\_超时\_LIVEDUMP**](bug-check-0x15c--pdc-watchdog-timeout-livedump.md)              
| 0x0000015D | [**SOC\_子系统\_故障\_LIVEDUMP**](bug-check-0x15d-soc-subsystem-failure-livedump.md)              
| 0x0000015E | [**BUGCODE\_NDIS\_驱动程序\_实时\_转储**](bug-check-0x15e-bugcode-ndis-driver-live-dump.md)                                                         |
| 0x0000015F | [**连接\_待机\_监视器\_超时\_LIVEDUMP**](bug-check-0x15f--connected-standby-watchdog-timeout-livedump.md)                            |
| 0x00000160 | [**WIN32K.SYS\_原子\_检查\_失败**](bug-check-0x160--win32k-atomic-check-failure.md)                                                             |
| 0x00000161 | [**实时\_系统\_转储**](bug-check-0x161--live-system-dump.md)                                                                                    |
| 0x00000162 | [**内核\_自动\_提升\_无效\_锁定\_版本**](bug-check-0x162--kernel-auto-boost-invalid-lock-release.md)                                     |
| 0x00000163 | [**辅助\_线程\_测试\_条件**](bug-check-0x162--worker-thread-test-condition.md)                                                           |
| 0x00000164 | [**WIN32K.SYS\_严重\_故障**](bug-check-0x164--win32k-critical-failure.md)                                                                      |
| 0x00000165 | [**群集\_CSV\_状态\_IO\_超时\_LIVEDUMP**](bug-check-0x165--cluster-csv-staus-io-timeout-livedump.md)                                      | 
| 0x00000166 | [**群集\_资源\_调用\_超时\_LIVEDUMP**](bug-check-0x166--cluster-resource-call-timeout-livedump.md)                                      |
| 0x00000167 | [**群集\_CSV\_快照\_设备\_信息\_超时\_LIVEDUMP**](bug-check-0x167--cluster-csv-snapshot-device-info-timeout-livedump.md)              |    
| 0x00000168 | [**群集\_CSV\_状态\_转换\_超时\_LIVEDUMP**](bug-check-0x168--cluster-csv-state-transition-timeout-livedump.md)                       |   
| 0x00000169 | [**群集\_CSV\_卷\_到达\_LIVEDUMP**](bug-check-0x169--cluster-csv-volume-arival-livedump.md)                                             |      
| 0x0000016A | [**群集\_CSV\_卷\_删除\_LIVEDUMP**](bug-check-0x16a--cluster-csv-volume-removal-livedump.md)                                            |    
| 0x0000016B | [**群集\_CSV\_群集\_监视器\_LIVEDUMP**](bug-check-0x16b--cluster-csv-cluster-watchdog-livedump.md)                                       |   
| 0x0000016C | [ **\_断开\_保护\_标记无效**](bug-check-0x16c--invalid-rundown-protection-flags.md)                                                   |
| 0x0000016D | [ **\_槽无效\_分配器\_标志**](bug-check-0x16d--invalid-slot-allocator-flags.md)                                                           |
| 0x0000016E | [**ERESOURCE\_无效\_版本**](bug-check-0x16e--eresource-invalid-release.md)                                                                  |
| 0x0000016F | [**群集\_CSV\_状态\_转换\_间隔\_超时\_LIVEDUMP**](bug-check-0x16f--cluster-csv-state-transistion-interval-livedump.md)           |
| 0x00000170 | [**加密\_库\_内部\_错误**](bug-check-0x170--crypto-library-internal-error.md)                                                         |
| 0x00000171 | [**群集\_CSV\_CLUSSVC\_断开\_监视器**](bug-check-0x171--cluster-csv-clussvc-disconnect-watchdog.md)                                    |
| 0x00000173 | [**COREMSGCALL\_内部\_错误**](bug-check-0x173--coremsgcall-internal-error.md)                                                                |
| 0x00000174 | [**COREMSG\_内部\_错误**](bug-check-0x174--coremsg-internal-error.md)                                                                        |
| 0x00000175 | [**先前\_严重\_异常\_重置\_错误**](bug-check-0x175--previous-fatal-abnormal-reset-error.md)                                            |
| 0x00000178 | [**检测到 ELAM\_驱动程序\_\_致命\_错误**](bug-check-0x175--elam-driver-detected-fatal-error.md)                                                  |
| 0x00000179 | [**群集\_CLUSPORT\_状态\_IO\_超时\_LIVEDUMP**](bug-check-0x179--cluster-clusport-status-io-timeout-livedump.md)                           |
| 0x0000017B | [**探查器\_配置\_非法**](bug-check-0x17b--profiler-configuration-illegal.md)                                                        | 
| 0x0000017C | [**PDC\_锁定\_监视器\_LIVEDUMP**](bug-check-0x17c--pdc-lock-watchdog-livedump.md)                                                               | 
| 0x0000017D | [**PDC\_意外\_吊销\_LIVEDUMP**](bug-check-0x17d-unexpected-revocation-livedump.md)                                                    | 
| 0x0000017E | [**微码\_修订版本\_不匹配**](bug-check-0x17e--microcode-revision-mismatch.md)                                                              | 
| 0x00000187 | [**视频\_DWMINIT\_超时\_回退\_BDD**](bug-check-0x187--video-dwminit-timeout-fallback-bdd.md)                                              |
| 0x00000188 | [**群集\_CSVFS\_LIVEDUMP**](bug-check-0x188--cluster-csvfs-livedump.md)                                                                        |
| 0x00000189 | [**错误的\_对象\_标头**](bug-check-0x189--bad-object-header.md)                                                                                  |
| 0x0000018B | [**安全\_内核\_错误**](bug-check-0x18b--secure-kernel-error.md)                                                                              |
| 0x0000018C | [**HYPERGUARD\_冲突**](bug-check-0x18c--hyperguard-violation.md)                                                                              |   
| 0x0000018D | [**安全\_错误\_未处理**](bug-check-0x18d--secure-fault-unhandled.md)                                                                        | 
| 0x0000018E | [**内核\_分区\_引用\_冲突**](bug-check-0x18e--kernel-partition-reference-violation.md)                                           |
| 0x00000190 | [**WIN32K.SYS\_严重\_故障\_LIVEDUMP**](bug-check-0x190--win32k-critical-failure-livedump.md)                                                   |
| 0x00000191 | [**检测到 PF\_检测到\_损坏**](bug-check-0x191--pf-detected-corruption.md)                                                                        |
| 0x00000192 | [**内核\_自动\_提升\_锁定\_获取\_，其中\_引发\_IRQL**](bug-check-0x192--kernel-auto-boost-lock-acquisition-with-raised-irql.md)         |
| 0x00000193 | [**视频\_DXGKRNL\_LIVEDUMP**](bug-check-0x192--video-dxgkrnl-livedump.md)                                                                        |
| 0x00000195 | [**SMB\_SERVER\_LIVEDUMP**](bug-check-0x195--smb-server-livedump.md)                                                                              |
| 0x00000196 | [**检测到\_回滚\_的加载程序**](bug-check-0x196--loader-rollback-detected.md)                                                                    |
| 0x00000197 | [**WIN32K.SYS\_安全\_失败**](bug-check-0x197--win32k-security-failure.md)                                                                      |
| 0x00000198 | [**UFX\_LIVEDUMP**](bug-check-0x198--ufx-livedump.md)                                                                                             |
| 0x00000199 | [ **\_使用的内核\_存储\_槽\_** ](bug-check-0x199--kernel-storage-slot-in-use.md)                                                              |
| 0x0000019A | [ **\_线程\_返回\_，同时\_将\_连接到\_接收器**](bug-check-0x19a--worker-thread-returned-while-attached-to-silo.md)                      |
| 0x0000019B | [**TTM\_致命\_错误**](bug-check-0x19b--ttm-fatal-error.md)                                                                                      |
| 0x0000019C | [**WIN32K.SYS\_POWER\_监视器\_超时**](bug-check-0x19c--win32k-power-watchdog-timeout.md)                                                         |
| 0x0000019D | [**群集\_SVHDX\_LIVEDUMP**](bug-check-0x19d--cluster-svhdx-livedump.md)                                                                        |
| 0x000001A0 | [**TTM\_监视器\_超时**](bug-check-0x1a0--ttm-watchdog-timeout.md)                                                                            |
| 0x000001A1 | [**WIN32K.SYS\_标注\_监视器\_LIVEDUMP**](bug-check-0x1a1--win32k-callout-watchdog-livedump.md)                                                   |
| 0x000001A2 | [**WIN32K.SYS\_标注\_监视器\_检测错误**](bug-check-0x1a2--win32k-callout-watchdog-bugcheck.md)                                                   |
| 0x000001A3 | [**调用\_\_未\_返回\_监视器\_超时\_LIVEDUMP**](bug-check-0x1a3--call-has-not-returned-watchdog-timeout-livedump.md)                  |
| 0x000001A4 | [**DRIPS\_SW\_HW\_分歧\_LIVEDUMP**](bug-check-0x1a4--drips-sw-hw-divergence-livedump.md)                                                    |
| 0x000001A5 | [**USB\_DRIPS\_阻止\_意外\_删除\_LIVEDUMP**](bug-check-0x1a5--usb-drips-blocker-surprise-removal-livedump.md)                           |
| 0x000001A6 | [**蓝牙\_错误\_恢复\_LIVEDUMP**](bug-check-0x1a6--bluetooth-error-recovery-livedump.md)                                                 |
| 0x000001A7 | [**SMB\_重定向程序\_LIVEDUMP**](bug-check-0x1A7--smb-redirector-livedump.md)                                                                      |
| 0x000001A8 | [**视频\_DXGKRNL\_黑色\_屏幕\_LIVEDUMP**](bug-check-0x1a8--video-dxgkrnl-black-screen-livedump.md)                                            |
| 0x000001B0 | [**VIDEO_MINIPORT_FAILED_LIVEDUMP**](bug-check-0x1b0--video-miniport-failed-livedump.md)                                                          |
| 0x000001B8 | [**VIDEO_MINIPORT_BLACK_SCREEN_LIVEDUMP**](bug-check-0x1b8--video-miniport-black-screen-livedump.md)                                              |
| 0x000001C4 | [**检测到\_验证程序\_检测到\_冲突\_LIVEDUMP**](bug-check-0x1c4--driver-verifier-detected-violation-livedump.md)                            |
| 0x000001C5 | [**IO\_THREADPOOL\_死锁\_LIVEDUMP**](bug-check-0x1c5--io-threadpool-deadlock-livedump.md)                                                     |
| 0x000001C6 | [**快速\_ERESOURCE\_前置条件\_冲突**](bug-check-0x1c6--fast-eresource-precondition-violation.md)                                         |
| 0x000001C7 | [**存储\_数据\_结构\_损坏**](bug-check-0x1c7--store-data-structure-corruption.md)                                                     |
| 0x000001C8 | [**手动\_启动\_电源\_按钮\_保持**](bug-check-0x1c8--manually-initiated-power-button-hold.md)                                          |
| 0x000001C9 | [**用户\_模式\_HEALTH\_监视器\_LIVEDUMP**](bug-check-0x1c9--user-mode-health-monitor-livedump.md)                                                |
| 0x000001CA | [**综合\_监视器\_超时**](bug-check-0x1ca--synthetic-watchdog-timeout.md)                                                                |
| 0x000001CB | [**分离\_接收器无效\_** ](bug-check-0x1cb--invalid-silo-detach.md)                                                                              |
| 0x000001CC | [**EXRESOURCE_TIMEOUT_LIVEDUMP**](bug-check-0x1cc--exresource-timeout-livedump.md)                                                                |
| 0x000001CD | [ **\_回调\_无效 STACK_ADDRESS**](bug-check-0x1cd--invalid-callback-stack-address.md)                                                        |
| 0x000001CE | [ **\_内核\_堆栈\_地址无效**](bug-check-0x1ce--invalid-kernel-stack-address.md)                                                           |
| 0x000001CF | [**硬件\_监视器\_超时**](bug-check-0x1cf--hardware-watchdog-timeout.md)                                                                  |  
| 0x000001D0 | [**CPI\_固件\_监视器\_超时**](bug-check-0x1d0--acpi-firmware-watchdog-timeout.md)                                                        |
| 0x000001D1 | [**遥测\_断言\_LIVEDUMP**](bug-check-0x1d1--telemetry-asserts-livedump.md)                                                                |
| 0x000001D2 | [**工作线程\_线程\_无效\_状态**](bug-check-0x1d2--worker-thread-invalid-state.md)                                                             |
| 0x000001D3 | [**WFP\_无效\_操作**](bug-check-0x1d3--wfp-invalid-operation.md)                                                                          |
| 0x000001D4 | [**UCMUCSI\_LIVEDUMP**](bug-check-0x1d4--ucmusci-livedump.md)                                                                                     |
| 0x000001D5 | [**DRIVER_PNP_WATCHDOG**](bug-check-0x1d5--driver-pnp-watchdog.md)                                                                                |
| 0x000001D6 | [**辅助\_线程\_返回\_，\_非\_默认\_工作负荷\_类**](bug-check-0x1d6--worker-thread-returned-with-non-default-workload-class.md)   |
| 0x000001D7 | [**EFS\_严重\_错误**](bug-check-0x1d7--efs-fatal-error.md)                                                                                      |
| 0x000001D8 | [**UCMUCSI\_故障**](bug-check-0x1d8--ucmucsi-failure.md)                                                                                       |
| 0x000001D9 | [**HAL\_IOMMU\_内部\_错误**](bug-check-0x1d8--ucmucsi-failure.md)                                                                            |  
| 0x000001DA | [* * HAL\_阻止\_处理器\_内部\_错误 * *](bug-check-0x1da--hal-blocked-processor-internal-error.md)                                         |
| 0x000001DB | [**IPI\_监视器\_超时**](bug-check-0x1db--ipi-watchdog-timeout.md)                                                                            |
| 0x000001DC | [**DMA_COMMON_BUFFER_VECTOR_ERROR**](bug-check-0x1dc--dma-common-buffer-vector-error.md)                                                          |
| 0x00000356 | [**XBOX\_ERACTRL\_CS\_超时**](bug-check-0x356--xbox-eractrl-cs-timeout.md)                                                                     |
| 0x00000BFE | [**BC\_蓝牙\_VERIFIER\_故障**](bug-check-0xbfe--bc-bluetooth-verifier-fault.md)                                                             |
| 0x00000BFF | [**BC\_BTHMINI\_VERIFIER\_错误**](bug-check-0xbff--bc-bthmini-verifier-fault.md)                                                                 |
| 0x00020001 | [**虚拟机监控程序\_错误**](bug-check-0x20001--hypervisor-error.md)                                                                                   |
| 0x1000007E | [**系统\_线程\_异常\_未\_处理\_M**](bug-check-0x1000007e--system-thread-exception-not-handled-m.md)                                  |
| 0x1000007F | [**意外\_内核\_模式\_陷阱\_M**](bug-check-0x1000007f--unexpected-kernel-mode-trap-m.md)                                                   |
| 0x1000008E | [**内核\_模式\_异常\_未\_处理\_M**](bug-check-0x1000008e--kernel-mode-exception-not-handled-m.md)                                      |
| 0x100000EA | [**线程\_停滞\_在\_设备\_驱动程序\_M**](bug-check-0x100000ea--thread-stuck-in-device-driver-m.md)                                              |
| 0x4000008A | [**线程\_终止\_持有\_互斥体**](bug-check-0x4000008a--thread-terminate-held-mutex.md)                                                        |
| 0xC0000218 | [**状态\_无法\_负载\_注册表\_文件**](bug-check-0xc0000218--status-cannot-load-registry-file.md)                                             |
| 0xC000021A | [**WINLOGON\_严重\_错误**](bug-check-0xc000021a--winlogin-fatal-error.md)                                              |
| 0xC0000221 | [**状态\_映像\_校验和\_不匹配**](bug-check-0xc0000221--status-image-checksum-mismatch.md)                                                  |
| 0xDEADDEAD | [**手动\_启动\_CRASH1**](bug-check-0xdeaddead--manually-initiated-crash1.md)                                                             |
